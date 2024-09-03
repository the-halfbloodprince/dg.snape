---
{"dg-publish":true,"permalink":"/learn/react/state-management/custom-observable-pattern-to-share-state/","noteIcon":""}
---

#react #observable-pattern #state-management #state-sharing #to-read

borrowed from: https://stackoverflow.com/a/62002044/12375141

# Custom [[Observable Pattern\|Observable Pattern]] to share state

It is possible without any external state management library. Just use a simple [observable](https://en.wikipedia.org/wiki/Observer_pattern) implementation:

```javascript
function makeObservable(target) {
  let listeners = []; // initial listeners can be passed an an argument aswell
  let value = target;

  function get() {
    return value;
  }

  function set(newValue) {
    if (value === newValue) return;
    value = newValue;
    listeners.forEach((l) => l(value));
  }

  function subscribe(listenerFunc) {
    listeners.push(listenerFunc);
    return () => unsubscribe(listenerFunc); // will be used inside React.useEffect
  }

  function unsubscribe(listenerFunc) {
    listeners = listeners.filter((l) => l !== listenerFunc);
  }

  return {
    get,
    set,
    subscribe,
  };
}
```

And then create a store and hook it to react by using `subscribe` in `useEffect`:

```javascript
const userStore = makeObservable({ name: "user", count: 0 });

const useUser = () => {
  const [user, setUser] = React.useState(userStore.get());

  React.useEffect(() => {
    return userStore.subscribe(setUser);
  }, []);

  const actions = React.useMemo(() => {
    return {
      setName: (name) => userStore.set({ ...user, name }),
      incrementCount: () => userStore.set({ ...user, count: user.count + 1 }),
      decrementCount: () => userStore.set({ ...user, count: user.count - 1 }),
    }
  }, [user])

  return {
    state: user,
    actions
  }
}
```

And that should work. No need for `React.Context` or lifting state up