## [< Back](../../../../)

```ts
/**
 * ClassNames util
 * Used to conditionally apply classes
 *
 * @param {String} classes Accepts strings
 */

function classNames(...classes: any) {
  return classes.filter(Boolean).join(" ");
}

export { classNames as cx };
```

## Usage

```jsx
function Demo() {
  const active = true;
  return (
    <div>
      <p className={cx("text-blue", active && "font-bold")}>This is a demo</p>
    </div>
  );
}

render(<Demo />);
```
