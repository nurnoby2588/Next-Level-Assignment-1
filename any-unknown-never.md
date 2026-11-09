# Understanding `any`, `unknown`, and `never`: Why `unknown` beats `any`

## Introduction
Typescript has different types with specific rules. Among them `unknown`, `never` and `any` have special roles. `unknown` accepts any value but required type checking before use, `nave` represent something that never happens and `any` disables type checking.

## The Top and Bottom Types
`unknown` is the **top type**: that can accept any value. `never` is the **bottom type**: it has no values, so it is assignable to every type. In contrast, `unknown` is assignable only to `unknown` and `any`.

```ts
function fail(message: string): never {
  throw new Error(message);
}
const n: number = fail("Oops"); // OK
```
## `any`: The Escape Hatch

`any` tells Typescript to skip type checking. It can be assigned to and from almost any type, so it sits outside the hierarchy.

```ts
let x: any = "hello";
x.foo.bar();     // runtime crash  
const n: number = x; // no error
```

## `unknown`: The Safe Alternative

`unknown` also accepts any value, but you must narrow it before using it.

```ts
let y: unknown = "hello";
y.toUpperCase(); //compile Error

if (typeof y === "string") {
  y.toUpperCase();  // OK
}
```

## Why choose `unknown` Over `any`
`any` hides bugs until they crash it runtime. `unknown` forces you to check types first, which suits `JSON.parse` results or form input. Also, `never` helps catch missing cases.

```ts
type Shape = "circle" | "square";
function area(s: Shape) {
  switch (s) {
    case "circle": return 1;
    case "square": return 2;
    default: { const check: never = s; return check; }
  }
}
```
## Conclusion
Use `unknown` to accept any value while keeping type sefety. Use `naver` for cases that should naver happend. Avoid `any` unless you really need it. Choosing the right type makes your code safer.