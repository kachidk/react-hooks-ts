## [< Back](../../../../)

```ts
import { useState, useEffect, ChangeEvent, useCallback, useMemo } from "react";

type InputChangeEvent = React.ChangeEvent<HTMLInputElement>;

type InputHandler = {
  /**
   * The current value of the input
   */
  value: any;

  /**
   * Function to handle onChange of an input element
   *
   * @param event The input change event
   */
  onChange: (e: InputChangeEvent) => void;
};

type Options = {
  /**
   * validate
   *
   * Validator function which can be used to prevent updates
   *
   * @param {any} New value
   * @param {any} Current value
   * @returns {boolean} Whether an update should happen or not
   *
   * */
  validate?: (newValue: any, currentValue: any) => boolean;
};

const defaultOptions: Options = {};

/**
 *
 * useInput Hook
 *
 * Handles an input's value and onChange props internally to
 * make text input creation process easier
 *
 * @param {any} [initialValue=""] Initial value of the input
 * @param {Options} [opts={}] Options object
 * @returns {InputHandler} Input handler with value and onChange
 */
function useInput(initialValue: any = "", options: Options = defaultOptions): InputHandler {
  const [value, setValue] = useState(initialValue);

  const onChange = useCallback(
    (e: InputChangeEvent) => {
      const newValue = e.target.value;
      let shouldUpdate = true;
      if (typeof options.validate === "function") {
        shouldUpdate = options.validate(newValue, value);
      }
      if (shouldUpdate) {
        setValue(newValue);
      }
    },
    [value]
  );

  // sync with default value
  useEffect(() => {
    setValue(initialValue);
  }, [initialValue]);

  const handler: InputHandler = {
    onChange,
    value,
  };

  return handler;
}

export { useInput };
```

## Usage

```ts
function Demo() {
  const myInput = useInput("hello");
  return (
    <div>
      <input {...myInput} />
      <p>
        Value is <b>{myInput.value}</b>
      </p>
    </div>
  );
}

render(<Demo />);
```

### With optional validator

```ts
function Demo() {
  const myInput = useInput("hello", {
    validate: (newValue) => newValue.length < 15,
  });
  return (
    <div>
      <p> Max length 15 </p>
      <input {...myInput} />
      <p>
        Value is <b>{myInput.value}</b>
      </p>
    </div>
  );
}

render(<Demo />);
```

### Arguments

| Argument     | Type   | Description                 | Default value |
| ------------ | ------ | --------------------------- | ------------- |
| initialValue | string | Initial value of the string | ""            |
| opts         | object | Options                     | {}            |

### Options

| Option key | Type     | Description                                                                                                             | Default value |
| ---------- | -------- | ----------------------------------------------------------------------------------------------------------------------- | ------------- |
| validate   | function | Validator function which receives changed valued before update as well as current value and should return true or false | undefined     |

### Return value

| Return value      | Type   | Description                                                                                                          |
| ----------------- | ------ | -------------------------------------------------------------------------------------------------------------------- |
| {value, onChange} | Object | Object containing {value : "String", onChange: "function that accepts an event and updates the value of the string"} |
