# Style guide

## General

- Use tabs.
- Use interfaces over types.
- Embrace simple for loops.
- Use `Uint8Array` over number arrays for representing bytes.
- Use classes when applicable.
- Avoid method chaining, abstract classes, and protected methods.
- Avoid complex type puzzles.
- Names functions over arrow functions.
  ```ts
  // bad
  const foo = () => {}

  // good
  function foo() {}
  ```

## Variable names

- Use camelCase for variables and functions, and SCREAMING_SNAKE_CASE for constants.
  ```ts
  let foo = 0;
  let fooBar = 0;
  const CONSTANT_VALUES_FOR_ALGORITHM = [1, 1, 1] as const;
  ```
- Use PascalCase case for types, interfaces, and classes.
  ```ts
  interface FooBar {
    a: string;
  }
  ```
- Variable names should not start with `is`, `has`, etc. Those should be limited to functions that return booleans.
- Avoid single letter variables.
- Acronyms should be in uppercase unless they're the first word in the name.

  ```ts
  function createHTTPServer(): void {
    // ...
  }

  let httpStatus: number;

  interface HTTPPOSTRequest {}
  ```

## Functions

- Explicit return types, even for functions that don't return values.

  ```ts
  // bad
  function foo(a: number) {
    // ...
  }

  // good
  function foo(a: number): number {
    // ...
  }

  function foo(a: number): void {
    // ...
  }
  ```

- Functions should be strict in what values they accept and return. Do not use union types except for representing multiple string literals.

  ```ts
  // bad
  function foo(a: string | number): string | number {
    // ...
  }

  // good
  function foo(a: string): string {
    // ...
  }

  function foo(a: "a" | "b"): void {
    // ...
  }
  ```

- No object parameters unless specified otherwise.

  ```ts
  // bad
  function foo(args: { a: string; b: string }): void {
    // ...
  }

  // good
  function foo(a: string, b: string): void {
    // ...
  }
  ```

- No optional parameters except for a single `options` object parameter.

  ```ts
  // bad
  function foo(a?: string): void {
    // ...
  }

  // good
  function foo(options?: { a?: string }): void {
    // ...
  }
  ```

- Avoid callback functions unless necessary. Reconsider the API design.
  ```ts
  // avoid
  function foo(onEvent: () => void): void {
    // ...
  }
  ```
- Avoid boolean parameters. If necessary, it should be an optional property in the `options` parameter though you should reconsider the API design.

  ```ts
  // bad
  function foo(a: boolean): void {
    // ...
  }

  // bad but better
  function foo(options?: { a?: boolean }): void {
    // ...
  }
  ```
