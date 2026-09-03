# Commit Message Generator

⬅️ [AI](AI.md)

Generate a Git commit command.

Adhere strictly to the Conventional Commits specification:
`type(scope): description`

## **`type`** (lowercase, imperative):

- `feat`: New feature or capability
- `fix`: Bug fix or error correction
- `refactor`: Code restructuring without changing behavior
- `docs`: Documentation updates
- `style`: Code formatting, semicolons, whitespace
- `test`: Test additions or corrections
- `chore`: Build process, tooling, maintenance
- `perf`: Performance improvements
- `ci`: CI/CD pipeline changes
- `build`: Dependency or build system changes

## **`scope`** (lowercase, concise):

- For monorepos: `frontend`, `backend`, `api`, `ui`, `database`, or specific component
- For simple repos: module name, component, or feature area
- Use `global` for cross-cutting changes affecting multiple areas

## **`description`** (imperative mood, concise, no period):

- Start with action verb
- Be specific but brief (50-72 chars ideal)
- Focus on what change does, not why

**Output format**: Only output the command as:

```bash
git commit -m "type(scope): description"
```
