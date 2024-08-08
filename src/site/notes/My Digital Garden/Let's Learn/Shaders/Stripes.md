---
{"dg-publish":true,"dg-path":"Let's Learn/Shaders/Stripes.md","permalink":"/let-s-learn/shaders/stripes/","noteIcon":""}
---

#shader #glsl #3D #webgl
### Arguments to the frag fn
the frag fn takes 4 arguments: 
1. **red** value, 
2. **green** value, 
3. **blue** value, and 
4. **opacity** value. 

All these values lie in the range [0.0, 1.0]. 
Any value above 1.0 is treated the same as 1.0
and any value below 0.0 is treated the same as 0.0.

eg:

`fragColor = vec4(1.0, 0.0, 0.0 ,1.0);`
will produce the following result:

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qz5p1cjziaatdgxn7b4e.png)

`fragColor = vec4(0.0, 1.0, 0.0 , 1.0);`
will produce the following result:

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/yzajvv9lq7a8ljosjfky.png)

`fragColor = vec4(0.0, 0.0, 1.0 , 1.0);`
will produce the following result:

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ctbtl5nii3ee3hlqo4ko.png)

You can mix the 4 fields with different values to generate any other colour or effect.

### Normalizing the coordinates to screen coordinates (uv)
```glsl
// Normalized pixel coordinates (from 0 to 1)
vec2 uv = fragCoord/iResolution.xy;

```

now `uv` will store a vec2 with values from 0 to 1 with the leftmost coordinate value 0 and rightmost value with value 1.

### Simple X-Gradient

```glsl
// Normalized pixel coordinates (from 0 to 1)
vec2 uv = fragCoord/iResolution.xy;


// Output to screen
fragColor = vec4(uv.x, 0.0, 0.0 , 1.0);

```

this will give the following result

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/t2z8ps0m5awo4ssehbai.png)

### Simple Y-Gradient

doing the same but with `uv.y`:

```glsl
// Normalized pixel coordinates (from 0 to 1)
vec2 uv = fragCoord/iResolution.xy;


// Output to screen
fragColor = vec4(uv.y, 0.0, 0.0 , 1.0);
```

output:

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kdgvh5aasm0jykz52sc3.png)

### Combining colors

We can combine the 3 fields to get different colours such as:
`fragColor = vec4(0.3, 0.0, 0.5 , 1.0);`
output:

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qejzsfz2bg581gsdf5lq.png)

### Stripes

to create stripes,
we start from a basic gradient:

```glsl
fragColor = vec4(uv.x, 0.0, 0.5 , 1.0);
```

output:

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/w35tu4zayz53mhc7e19c.png)

right now the red value is varying linearly along the x-direction.

Lets start by choosing a function which oscillates unlike a linear function.

eg: sine function

`fragColor = vec4(sin(uv.x), 0.0, 0.5 , 1.0);`

output:

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/7c6xnpmkbu6rwuis7k09.png)

you may not be able to tell a lot of difference, but wait until we scale the input to the function:

for a linear func: `fragColor = vec4(uv.x * 20.0, 0.0, 0.5 , 1.0);`

output:

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/9rmpw02lzrb25l3uy9yj.png)

but for the sine func: fragColor = vec4(sin(uv.x * 20.0), 0.0, 0.5 , 1.0);

output:

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/0k72v01lnxikxuup0pws.png)

as we see the red value for linear fn reaches 1 faster and then above 1 it behaves as 1, but for the oscillatory fn reaches 1 very fast and then again goes to -1, which is why we see the darker region more as values < 0 are treated as 0.

to get a more equal width strip pattern, we need to oscillate the values from 0 to 1 not -1 to 1.

for this lets try using the following trick
remove the -1 part by adding 1 to the func , ie, `sin(uv.x) + 1.`

but this will get us the answer from 0 to 2.

to manage this, we can halve this, ie, 0.5 * (sin(uv.x * 20.) + 1.)

output:

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/dd6vjd2nofeb0tcqoq19.png)

increasing the argument to sine func increases the frequency of the stripes and reduces the width:

eg: changing the scale from 20. to 40.
`fragColor = vec4(0.5 * (sin(uv.x * 40.) + 1.), 0.0, 0.5 , 1.0)`

output:

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/uu6u7msik0udl0f5m9a4.png)

to make the strips sharp and not dissolving naturally, we can ceil the sine func which will give us values in sharp 0 and 1.

```
fragColor = vec4(ceil(sin(uv.x * 40.)), 0.0, 0.5 , 1.0);
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5pvbpaii0clxzh8ke3yo.png)

#### Y-stripes

replacing `uv.x` in the above expression with `uv.y` gives us stripes along the y-direction

`fragColor = vec4(0.5 * (sin(uv.y * 40.) + 1.), 0.0, 0.5 , 1.0);`

output:

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/770nkzigjir3mo1ia61a.png)

```
fragColor = vec4(ceil(sin(uv.x * 40.)), 0.0, 0.5 , 1.0);
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/4mi181w2fkip45imrygg.png)

combining the x and y expressions:
`fragColor = vec4(0.5 * (sin(uv.y * 40.) + 1.) + 0.5 * (sin(uv.x * 40.) + 1.), 0.0, 0.5 , 1.0);`

output:

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/s0vpkvk7k1q01wdc00yq.png)

sharpening the values:
```glsl
fragColor = vec4(ceil(sin(uv.y * 40.)) + ceil(sin(uv.x * 40.)), 0.0, 0.5 , 1.0);
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/hi6r7wa1ako08nkxkbvv.png)

keeping the red stripes in x and blue stripes in y, we get:
`fragColor = vec4(0.5 * (sin(uv.x * 40.) + 1.), 0.0, 0.5 * (sin(uv.y * 40.) + 1.) , 1.0);`

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/1o59g4gov2socznjb963.png)

`fragColor = vec4(ceil(sin(uv.x * 40.)), 0.0, ceil(sin(uv.y * 40.)) , 1.0);`

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/1z818fdhn3tfyx7myt6q.png)