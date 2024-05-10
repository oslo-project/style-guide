# Style guide

## General

- Use tabs.
- Use interfaces instead of types.
- Use `"` instead of `'`.
- Use `let` and `const` instead of `var`.
- Use classes when applicable.
- `await` instead of `.then`.
- Separate type and regular imports.

  ```ts
  // bad
  import { someFunction, SomeType } from "foo";
  import { someFunction, type SomeType } from "foo";

  // good
  import { someFunction } from "foo";
  import type { SomeType } from "foo";
  ```

- Mutability is fine.
- Use `Uint8Array` instead of number arrays for representing bytes.

## Naming convention

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

- Use named functions instead of arrow functions for top-level function.

  ```ts
  // bad
  const foo = () => {};

  // good
  function foo() {}
  ```

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

- Throw errors. Don't return them.
- Avoid complex type puzzles.

## Control flow

### If statements

- Use `{}`.

  ```ts
  // bad
  if (condition) stuff;

  // good
  if (condition) {
    stuff;
  }
  ```

- Use shortcuts only for booleans.

  ```ts
  let foo: string;

  // bad
  if (!foo) {
    // ...
  }

  // good
  if (foo !== "") {
    // ...
  }
  ```

- Never use `==` or `!=`.

### Other

- Embrace simple `for` loops. Don't try to force `.map()` and don't use `.forEach()`.
- Avoid switch statements.
- Avoid `finally`.

## Classes

- Avoid method chaining, abstract classes, and protected methods.
- No getters and setters.
- No static methods and properties.
- Properties, constructor, methods - in that order.
- Inheritance is ok but avoid overriding methods and properties.
