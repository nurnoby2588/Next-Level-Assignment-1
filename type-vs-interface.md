# Type Aliases vs Interface in TypeScript: Differences and when to choose Each

## Introduction
In TypeScript, both `type` and `interface` define structure of your data and give type safety. They look similar,but have some key difference. Let's explore those differences and when to use each one.

## Similarities

Both `type` and `interface` can describe with object shape and both can be extended. An interface uses extends keyword, on the other hand a type uses &

```typescript
type UserType = { name: string; age: number };
interface UserInterface {
  name: string;
  age: number;
}
type AdminType = UserType & { role: string };
interface AdminInterface extends UserInterface {
  role: string;
}
```

Both `AdminType` and `AdminInterface` have `name`, `age` and `role`

## Declaration Merging

Declaration merging works only with `interface`. If you declare two interface with the same name, TypeScript automatically merge them into one. But `type` can't do this, the same type name gives a compile error

```typescript
interface Settings {
  theme: string;
}
interface Settings {
  language: string;
}

type Config = { theme: string };
type Config = { language: string }; // Error: Duplicate indentifier Config
```

## What Only `type` Can Do

A `type` can also describe unions ,tuple and literal. which an `interface` can't express directly. That's way type is more flexible then interface when working non-object data.

```typescript
type Id = string | number;
type Point = [number, number];
type Status = "active" | "inactive";
```

Each of these shapes cannot be written with an `interface`

## Conclusion

Use `interface` for object shape, classes and public APIs because it support extends and declaration merging. Use `type` for unions, tuple, literal types. Both work with simple object.
