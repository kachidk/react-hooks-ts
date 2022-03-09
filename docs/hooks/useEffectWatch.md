## [< Back](../../../../)

React effect hook that ignores the first invocation (e.g. on mount).
The signature is exactly the same as the useEffect hook.

```ts
import { useEffect, useRef } from "react";

const useUpdateEffect: typeof useEffect = (effect, deps) => {
  const isFirstMount = useFirstMountState();

  useEffect(() => {
    if (!isFirstMount) {
      return effect();
    }
  }, deps);
};

function useFirstMountState(): boolean {
  const isFirst = useRef(true);

  if (isFirst.current) {
    isFirst.current = false;

    return true;
  }

  return isFirst.current;
}

export default useUpdateEffect;
```
