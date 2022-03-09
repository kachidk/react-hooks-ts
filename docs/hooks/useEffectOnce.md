## [< Back](../../../../)

React lifecycle hook that runs an effect only once. It has the same signature as `React.useEffect`.

```ts
import { EffectCallback, useEffect } from "react";

const useEffectOnce = (effect: EffectCallback) => {
  useEffect(effect, []);
};

export default useEffectOnce;
```
