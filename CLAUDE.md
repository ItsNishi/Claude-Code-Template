# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Code Style

### Formatting
- **Indentation**: Tabs (not spaces)
- **Bracing**: Allman style (opening brace on its own line)
- **Line length**: 100 soft limit, 120 hard limit -- break at logical points
- **Blank lines**: One between methods, two between sections/classes

```c
void Example_Function()
{
	if (Condition)
	{
		Do_Something();
	}
}
```

### Naming
- **PascalCase** for types, functions, and general identifiers
- **Pascal_Snake_Case** where word separation improves readability

### Comments
- Prefer `//` over block comments
- TODO format: `// TODO: Description (#issue)`

### Readability
- Guard clauses over deep nesting -- return early instead of wrapping in conditionals
- No magic numbers/strings -- extract to named constants
- Keep functions focused -- if it needs scrolling, split it
- 3-4 parameters max -- beyond that, use a config object

### Dead Code
- Delete it if git tracks the project (history exists for recovery)
- Comment with a reason if no version control

## Design Principles

- Single responsibility -- one class, one reason to change
- Composition over inheritance
- Constructor injection for dependencies

## Interaction Style

- Challenge suboptimal approaches -- suggest better alternatives with reasoning
- Accept user override after presenting the case
- Keep explanations concise: bullets and short sentences over paragraphs
- Lead with code, follow with explanation if needed

## Language Preferences

<!-- Keep the languages you use, delete the rest, add your own -->

### Python
- Tabs for indentation
- PascalCase for classes, snake_case for functions/variables
- Type hints, double quotes, f-strings

### JavaScript / TypeScript
- Tabs for indentation
- camelCase for variables/functions, PascalCase for classes/types
- Prefer `const` over `let`, no `var`
- Arrow functions for callbacks

### C#
- Tabs for indentation
- PascalCase for public members, _PascalCase for private fields
- `var` when type is obvious from right-hand side
- File-scoped namespaces, string interpolation over concatenation

### C/C++
- Tabs for indentation
- `#pragma once` over include guards
- Smart pointers over raw `new`/`delete`
- `const` correctness expected

<!-- ## Git Conventions

- Privacy email: `<id>+<user>@users.noreply.github.com`
- SSH remotes: `git@github.com:<user>/<repo>.git`
- Pull before push: `git pull --rebase origin main`
-->

<!-- ## Security Context

- Offensive security tools are authorized (pentest/CTF context)
- Flag potential vulnerabilities in code reviews
-->

<!-- ## Testing Preferences

- Prefer [unit/integration/e2e] tests
- Use [framework] for [language]
- Test naming: [convention]
-->

## Restrictions

- No emojis in code or communication
