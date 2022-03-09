## [< Back](../../../../)

```ts
import { useEffect } from "react";

/**
 * useWillUnmount hook
 * Fires a callback just before component unmounts
 *
 * @param {Function} callback Callback to be called before unmount
 */
function useWillUnmount(callback: () => any): void {
  // run only once
  useEffect(() => {
    return callback;
  }, []);
}

export default useWillUnmount;
```

## Usage

```jsx
function Message() {
  useWillUnmount(function () {
    alert("unmounted");
  });
  return <p> Message </p>;
}

function Demo() {
  const [value, changeValue] = useState(true);

  function toggleValue() {
    changeValue(!value);
  }

  return (
    <>
      <p>
        <button onClick={toggleValue}>Toggle show </button>
      </p>
      {value && <Message />}
    </>
  );
}

render(<Demo />);
```

## Arguments

| Arguments | Type     | Description                                     | Default value |
| --------- | -------- | ----------------------------------------------- | ------------- |
| callback  | function | Callback function which needs to run on unmount | undefined     |
