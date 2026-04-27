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

Use `name=value` (e.g., `myvar=5`). There is No need for `var` or `let` for basic string or integer assignment.