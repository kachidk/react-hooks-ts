## [< Back](../../../../)

```ts
import { useEffect } from "react";

/**
 * useDidMount hook
 * Calls a function on mount
 *
 * @param {Function} callback Callback function to be called on mount
 */
function useDidMount(callback: () => any): void {
  useEffect(() => {
    if (typeof callback === "function") {
      callback();
    }
  }, []);
}

export default useDidMount;
```

## Usage

```jsx
function Demo() {
  useDidMount(function () {
    console.log("mounted");
  });
  return null;
}

render(<Demo />);
```

## Arguments

| Argument | Type     | Description                    |
| -------- | -------- | ------------------------------ |
| callback | function | function to be called on mount |
