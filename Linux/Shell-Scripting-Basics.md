# Shell Scripting Basics

I'm gonna use js examples side by side so that it will be easy for me to understand.

## File Name

- Use **Descriptive Names** such as `deploy_app.sh` or `cleanup_logs.sh`.
- Recommended: use underscores (`_`) for word separators in filenames.

## Baby Step

Showing someting on the terminal.

**Bash**:

```bash
echo "Hello World";
```

**JS**:

```js
console.log("Hello World");
```

## Variable Naming Convention Rules

Variable names can only contain:

- **Letters** (a-z, A-Z)
- **Numbers** (0-9)
- **Underscore** (\_)

> Spaces and special characters like `@`, `#`, `$`, `!`, `-` are **not allowed** (except underscore).

The first character must be:

- A **letter** (a-z, A-Z), or
- An **underscore** (\_)

Variable names **cannot start with a number**.

Example: `1var=10` is invalid; use `var1=10` instead.

## Variable Assignment

Use `key=value` (e.g., `myvar=5`).

Therefore, you should use `name=value` for general variables and `readonly` for constants in Bash

| Keyword (JS)  | Bash Equivalent       | Purpose                       |
| ------------- | --------------------- | ----------------------------- |
| `var` / `let` | `name=value`          | Declare and assign a variable |
| `const`       | `readonly name=value` | Declare a read-only constant  |
