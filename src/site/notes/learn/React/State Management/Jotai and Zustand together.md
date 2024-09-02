---
{"dg-publish":true,"permalink":"/learn/react/state-management/jotai-and-zustand-together/","noteIcon":""}
---

# Jotai and Zustand together: Chat with ChatGPT
## is it wise to use [[jotai\|jotai]] and [[zustand\|zustand]] together?
Using Jotai and Zustand together can be beneficial, depending on your application's needs. Both libraries are lightweight state management solutions, but they serve slightly different purposes:

- **Zustand**: Primarily used for managing global state, it is well-suited for scenarios where you need to share state across multiple components or manage more complex state logic, like asynchronous actions.

- **Jotai**: Focuses on atomic state management, where each piece of state is represented as an atom. It allows for fine-grained reactivity, meaning components only re-render when the specific atoms they depend on change.

### When to Use Both Together
- **Granular State Management**: You can use Jotai for more granular, isolated pieces of state while using Zustand for broader application-wide state management. This allows you to leverage the strengths of each library where they make the most sense.
  
- **Ease of Migration**: If you're already using one of the libraries and want to incorporate the other, they can work together without much friction. You can gradually introduce one into your project without needing to refactor everything.

- **Scalability**: In larger applications, combining both can help keep your state management organized. Use Zustand for high-level state that needs to be accessed globally and Jotai for more detailed or component-specific state.

### Things to Consider
- **Complexity**: Introducing both libraries can add a layer of complexity to your codebase. Make sure there's a clear reason for using both to avoid confusion among team members.

- **Performance**: While both libraries are performant, using two state management libraries might introduce overhead. However, this is generally negligible unless you're working on a performance-critical application.

### Conclusion
If your application requires both fine-grained state control and broader global state management, using Jotai and Zustand together can be a wise choice. Just be mindful of the added complexity and ensure that it’s necessary for your specific use case.

## give me a size comparison of using the two together vs using redux with redux toolkit
When comparing the size of using Jotai and Zustand together versus using Redux with Redux Toolkit, here’s a general overview:

### Bundle Size Overview (self research with Bundlephobia and GPT)

#### Zustand
![Pasted image 20240902192134.png](/img/user/learn/React/State%20Management/Pasted%20image%2020240902192134.png)
#### Jotai
![Pasted image 20240902192154.png](/img/user/learn/React/State%20Management/Pasted%20image%2020240902192154.png)
#### redux
![Pasted image 20240902192208.png](/img/user/learn/React/State%20Management/Pasted%20image%2020240902192208.png)
#### redux toolkit
![Pasted image 20240902192311.png](/img/user/learn/React/State%20Management/Pasted%20image%2020240902192311.png)
#### react-redux
![Pasted image 20240902192346.png](/img/user/learn/React/State%20Management/Pasted%20image%2020240902192346.png)

#### GPT's answer
1. **Zustand + Jotai**:
   - **Zustand**: Around 2 KB minified + gzipped.
   - **Jotai**: Around 3.5 KB minified + gzipped.
   - **Combined**: Approximately 5.5 KB minified + gzipped.

2. **Redux + Redux Toolkit**:
   - **Redux**: Around 6.7 KB minified + gzipped.
   - **Redux Toolkit**: Adds around 8 KB minified + gzipped.
   - **Combined**: Approximately 14.7 KB minified + gzipped.

### Comparison

- **Zustand + Jotai (5.5 KB)** is significantly smaller than **Redux + Redux Toolkit (14.7 KB)**, making it a lighter choice in terms of bundle size.

### Considerations Beyond Size

- **Functionality**: Redux with Redux Toolkit offers a robust ecosystem with features like middleware, DevTools integration, and a clear structure for large-scale applications. Zustand and Jotai are more minimalistic, focusing on simplicity and performance.
  
- **Complexity**: Zustand and Jotai are simpler to set up and use, especially for smaller or mid-sized applications. Redux with Redux Toolkit provides more structure, which can be beneficial in larger projects but might introduce unnecessary complexity in smaller ones.

- **Performance**: The smaller bundle size of Zustand and Jotai may contribute to faster load times, especially in smaller applications. However, Redux's performance is generally strong, and the difference might be negligible in larger apps where other factors dominate.

### Conclusion

Using Jotai and Zustand together results in a smaller bundle size compared to using Redux with Redux Toolkit. If bundle size is a priority and your application doesn't require the full feature set of Redux, the Jotai + Zustand combination could be a more efficient choice. However, if you need the advanced features and ecosystem that Redux offers, the larger size might be justified.