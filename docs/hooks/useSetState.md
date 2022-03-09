## [< Back](../../../../)

React state hook that creates setState method which works similar to how
this.setState works in class components—it merges object changes into
current state.

```ts
import { useCallback, useState } from "react";

/**
 * useSetState hooks
 * Used to merge object changes into current state.
 *
 * @param {Object} initialState Accepts Objects
 */

const useSetState = <T extends object>(initialState: T = {} as T): [T, (patch: Partial<T> | ((prevState: T) => Partial<T>)) => void] => {
  const [state, set] = useState<T>(initialState);
  const setState = useCallback((patch) => {
    set((prevState) => Object.assign({}, prevState, patch instanceof Function ? patch(prevState) : patch));
  }, []);

  return [state, setState];
};

export default useSetState;
```

## Usage

```jsx
const [state, setState] = useSetState({ count: 0 });

setState({ count: state.count + 1 });
setState((prevState) => ({
  count: prevState + 1,
}));
```
