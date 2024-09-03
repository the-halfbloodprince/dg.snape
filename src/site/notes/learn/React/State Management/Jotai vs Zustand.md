---
{"dg-publish":true,"permalink":"/learn/react/state-management/jotai-vs-zustand/","noteIcon":""}
---

### Resources
- https://youtu.be/5-1LM2NySR0?si=b6vne5zIruWWG7bm&t=1504
- https://www.reddit.com/r/reactjs/comments/1ctsnov/why_choose_zustand_over_jotai/


![Pasted image 20240902175827.png](/img/user/learn/React/State%20Management/Pasted%20image%2020240902175827.png)

### [[Jotai\|Jotai]]
- very good for almost everything
- if you need to expose specific functions etc and not any mutation, then you'll need an extra layer
- whichever atom needs change, just update that
- simply for shared state

### [[Zustand\|Zustand]]
- single store
- well defined mutations
- example: ![Pasted image 20240902180346.png](/img/user/learn/React/State%20Management/Pasted%20image%2020240902180346.png)
- not a shared state but a well defined machine
- say we have a state with multiple keys in it, and we just want to subscribe to one specific key in the object
- if we are selecting that key this will only update when that key changes
- but if we use say a method in the [[zustand\|zustand]] store, that component won't update
- can be natively used without [[learn/React/React\|React]] as well (externally managed data which is internally operated)

### Why [[Zustand\|Zustand]] preferred over [[Jotai\|Jotai]] mostly?
https://www.reddit.com/r/reactjs/comments/1ctsnov/why_choose_zustand_over_jotai/

>They can pretty much do the same things as the other, it's more of the mental model that might change. Zustand is viewed as more of a global store while Jotai has individual functions/atoms. Keep in mind that Zustand can have context and small stores while Jotai can become global.
>
>The reason why Zustand is more popular has nothing to do with which is better imo. Zustand came out before Jotai and was a compelling alternative to Redux. While Jotai is also an alternative, it's not seen as a direct alternative. Since most people have heard of or worked with Redux, they're more likely to try Zustand than Jotai. Also, Jotai, while not as popular as Zustand, is still gaining more and more popularity.


>>Zustand is viewed as more of a global store while Jotai has individual functions/atoms.
> 
> While this has little impact in single-person projects, it becomes **huge** in large teams.
>
>The issue is that Jotai uses free mini-stores (atoms), which you can organize (or _not_ organize) the way you want. Now, everyone who ever worked in a large team knows that this has the potential to become a huge mess really quick.
> 
>Zustand, in the other hand, _forces_ a structure upon your store. Even if you have multiple stores, they will look like somewhat alike. And this keeps the whole code easier to maintain.
> 
>I work in an enterprise environment, and that's why we use Zustand.

>They’re made by the same dev to solve different problems. Zustand is top-down and Jotai is bottom-up.
>
>Think of a dashboard. With zustand you can store and manage the theme/color, settings, websocket connections, etc. (from the top)
>
>Now let’s say you have a bunch of interactive components such as charts, tables, graphs, etc. and they each have their state. Jotai would be useful here because you can manage their state atomically (from the bottom). This means that if some components reference the state in other ones, you can easily access them with Jotai. Jotai also handles rapidly changing data and computed/derived values better. You could use Zustand as well for this, but as your application becomes more complex, it’s a lot easier to handle and manage the state in the component versus globally.
>
>There’s a few other technical differences, but overall it’s going to depend what you’re building. If you’re still not sure, just start with Zustand for global stuff and useState for components. You’ll know when you need Jotai.
>
>[this video](https://youtu.be/5-1LM2NySR0) explains it a lot better.

### A really good example for [[Jotai\|Jotai]] vs [[learn/React/State Management/React Context\|React Context]]
https://www.reddit.com/r/reactjs/comments/1ctsnov/comment/l4fpweu/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button

>Everything you said is right, but I feel like it helps to show a specific situation
>
>Let's say that you a chart component (Component A). It has rapidly-changing state, but the component is a leaf node, so the constant re-renders aren't a huge deal
>
>Now let's say that you need to share that state with another component (Component B). If B is a sibling of A, then the traditional React solution is to lift the state up to the shared parent, and pass it down to the two child nodes. Depending on what the parent is doing, this may be good or bad – it might be computationally costly for the parent to re-render as often as Competent A, but realistically, it still won't be a huge deal
>
>Now let's say that Competent A and Component B still need to share state, but they're not direct siblings anymore – they're on opposite ends of the UI tree, and the only common parent is the top-level App component. This is where React's default mental model starts to break down – if you lift the state all the way to the top of the app, all the re-renders from Component A's state changes will wreak havoc and make the app performance slow to a crawl. The whole app will be re-rendering constantly, even if 99% of the UI doesn't change at all. It doesn't matter whether the state is exposed via props or context – any state changes to the app will make all of its direct children re-render too
>
>Now, you could use React's memoization tools, but they're clunky, and hard to get right. So Jotai instead asks "What if we break the state outside of React, and let components subscribe to it?" That way, Component A and Component B can use it directly, but because none of the other components even know about it, they don't re-render when the state changes
>
>With Jotai, it doesn't matter where the state is used. It lives outside React, so any number of components can use it without affecting how often other components re-render

https://www.reddit.com/r/reactjs/comments/1ctsnov/comment/l4eh6o9/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button