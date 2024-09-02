---
{"dg-publish":true,"permalink":"/learn/react/state-management/jotai-vs-zustand/","noteIcon":""}
---

### Resources
- https://youtu.be/5-1LM2NySR0?si=b6vne5zIruWWG7bm&t=1504


![Pasted image 20240902175827.png](/img/user/learn/React/State%20Management/Pasted%20image%2020240902175827.png)

### Jotai
- very good for almost everything
- if you need to expose specific functions etc and not any mutation, then you'll need an extra layer
- whichever atom needs change, just update that
- simply for shared state

### Zustand
- single store
- well defined mutations
- example: ![Pasted image 20240902180346.png](/img/user/learn/React/State%20Management/Pasted%20image%2020240902180346.png)
- not a shared state but a well defined machine
- say we have a state with multiple keys in it, and we just want to subscribe to one specific key in the object
- if we are using that key this will only update when that key changes