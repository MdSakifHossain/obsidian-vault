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

## Variable Naming

Variable Names should remail lowercase (e.g., `file_count`, `backup_dir`).

## Variable Assignment

Use `key=value` (e.g., `myvar=5`). 

Therefore, you should use `name=value` for general variables and `readonly` for constants in Bash

| Keyword (JS)  | Bash Equivalent       | Purpose                       |
| ------------- | --------------------- | ----------------------------- |
| `var` / `let` | `name=value`          | Declare and assign a variable |
| `const`       | `readonly name=value` | Declare a read-only constant  |
|               |                       |                               |
