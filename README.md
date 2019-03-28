# All the credit goes to @xnimorz

This is a reworked copy of `use-debounce` library from @xnimorz (https://github.com/xnimorz/use-debounce) for "preact".

The code of the hook is the same, except switching from react to preact package.

## useDebounce preact hook

Install it with yarn:

```
yarn add use-debounce-preact
```

Or with npm:

```
npm i use-debounce-preact --save
```

## Simple debouncing

```javascript
/** @jsx h */
import { h } from 'preact';
import { useState } from 'preact/hooks';
import { useDebounce } from 'use-debounce-preact';

export default function Input() {
  const [text, setText] = useState('Hello');
  const [value] = useDebounce(text, 1000);

  return (
    <div>
      <input
        defaultValue={'Hello'}
        onInput={(e) => {
          setText(e.target.value);
        }}
      />
      <p>Actual value: {text}</p>
      <p>Debounce value: {value}</p>
    </div>
  );
}
```

## Debounced callbacks

Besides `useDebounce` for values you can debounce callbacks, that is the more commonly understood kind of debouncing.

```js
import useDebouncedCallback from 'use-debounce-preact/lib/callback';

function Input({ defaultValue }) {
  const [value, setValue] = useState(defaultValue);
  // Debounce callback
  const [debouncedCallback] = useDebouncedCallback(
    // function
    (value) => {
      setValue(value);
    },
    // delay in ms
    1000,
    // deps (in case your function has closure dependency like https://reactjs.org/docs/hooks-reference.html#usecallback)
    []
  );

  // you should use `e => debouncedCallback(e.target.value)` as react works with synthetic evens
  return (
    <div>
      <input
        defaultValue={defaultValue}
        onInput={(e) => debouncedCallback(e.target.value)}
      />
      <p>Debounced value: {value}</p>
    </div>
  );
}
```
