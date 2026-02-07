# CLAUDE.md Template

A customizable configuration file for [Claude Code](https://claude.ai/code) to define your coding personality and preferences.

---

## 🎯 What is This?

This file tells Claude Code how you like to work. Drop it in your project root and Claude will follow your coding style, communication preferences, and conventions automatically.

## 📋 Template

````markdown
# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Code Style

### Indentation
- Use **Allman style** bracing (opening brace on its own line)
- Use **tabs** for indentation, not spaces

```c
void Example_Function()
{
	if (Condition)
	{
		Do_Something();
	}
}
```

### Naming Conventions
- Use **PascalCase** for types, functions, and general identifiers
- Use **Pascal_Snake_Case** for functions and variables where word separation improves readability

### Comments
- Prefer single-line comments (`//`) over block comments
- When modifying existing code, wrap the old code in a multi-line comment with an explanation:

```c
/*
Old_Implementation();
Reason: Replaced due to performance issues with large datasets
*/
New_Implementation();
```

- TODO format: `// TODO: Description (#issue)` or `# TODO: Description`

### Line Length
- Soft limit: **100 characters**
- Hard limit: **120 characters**
- Break long lines at logical points (after commas, before operators)

### File Organization
- One primary type per file
- File name matches the type name (e.g., `Port_Scanner.cs` contains `Port_Scanner`)
- Using/import ordering: system/stdlib first, third-party second, project-local third, separated by blank lines

### Readability
- **Guard clauses over deep nesting** -- return/throw early at the top instead of wrapping the entire function body in conditionals
- **No magic numbers/strings** -- extract to named constants (`Max_Retries` over `3`, `Default_Timeout` over `5000`)
- **Keep functions focused** -- if a function needs scrolling, it probably needs splitting
- **Parameter count** -- more than 3-4 parameters suggests the function needs a config object or refactoring
- **Blank lines** -- one blank line between methods, two between sections/classes

### Dead Code
- If the project uses git, delete dead code -- git history exists for recovery
- If the project does **not** use git, comment out dead code with a reason instead of deleting

### Code Structure

#### Class/Type Member Ordering

Organize members in a consistent order within every type:

1. Constants
2. Static fields
3. Instance fields
4. Constructors
5. Properties
6. Public methods
7. Protected methods
8. Private methods
9. Nested types

```csharp
public class Example_Service
{
	// 1. Constants
	private const int Default_Timeout = 5000;

	// 2. Static fields
	private static readonly Dictionary<int, string> _Service_Map = new();

	// 3. Instance fields
	private readonly ILogger _Logger;
	private int _Counter;

	// 4. Constructors
	public Example_Service(ILogger Logger)
	{
		_Logger = Logger;
	}

	// 5. Properties
	public string Name { get; set; } = string.Empty;

	// 6. Public methods
	public void Execute() { }

	// 7. Protected methods
	protected virtual void On_Executing() { }

	// 8. Private methods
	private void Initialize() { }

	// 9. Nested types
	private class Internal_Helper { }
}
```

### Object Lifetime and Resource Management

#### C#
- Use `using` statements / declarations for `IDisposable` resources (streams, connections, HttpClient)
- Implement `IDisposable` when your class holds unmanaged resources or other disposables
- Prefer `using var` declarations over `using` blocks when scope is the entire method

#### C/C++
- RAII -- acquire resources in constructors, release in destructors
- Smart pointers (`std::unique_ptr`, `std::shared_ptr`) over raw `new`/`delete`
- Free what you allocate; null what you free

#### Rust
- Ownership and borrowing are enforced by the compiler
- Document safety invariants on every `unsafe` block
- Prefer borrowing (`&T`, `&mut T`) over cloning

#### Python
- Context managers (`with` statements) for files, connections, locks
- Close resources explicitly when context managers aren't available

### Design Principles
- **Single responsibility** -- one class, one reason to change; if it keeps growing, split it
- **Composition over inheritance** -- unless there's a clear "is-a" relationship
- **Small focused interfaces** -- prefer several specific interfaces over one large one
- **Constructor injection** for dependencies -- avoid service locator or static access patterns
- **Encapsulate what varies** -- isolate the parts that change behind interfaces

## Interaction Style

### Feedback Approach
- Challenge suboptimal approaches and suggest better alternatives
- Do not simply agree with user decisions if a better solution exists
- Provide direct critique with reasoning
- Accept user override after presenting the case

### Communication Format
- Keep explanations concise with clear structure
- Use bullet points and short sentences over dense paragraphs
- Lead with code examples, follow with explanation if needed
- Avoid walls of text

## Language-Specific Preferences

### C#
- Tabs for indentation
- PascalCase for public members, _PascalCase for private fields
- Prefer `var` when type is obvious from right-hand side
- Use `string.Empty` over `""`
- Prefer string interpolation `$"{Value}"` over concatenation
- File-scoped namespaces

### Python
- Tabs for indentation (override PEP 8)
- PascalCase for classes, Pascal_Snake_Case for functions and variables (override PEP 8)
- Use type hints
- Double quotes for strings
- f-strings for formatting

### C/C++
- Tabs for indentation
- `#pragma once` over include guards
- Pointer asterisk attached to type: `int* Ptr` not `int *Ptr`
- Prefer smart pointers (`std::unique_ptr`, `std::shared_ptr`) over raw pointers
- `const` correctness is expected
- Include order: local headers, project headers, system headers

### Rust
- Tabs for indentation
- Opening brace on same line (Rust convention, overrides Allman)
- PascalCase for types, traits, enums, enum variants
- snake_case for functions, methods, variables, modules (Rust convention)
- SCREAMING_SNAKE_CASE for constants
- `///` doc comments for public API, `//` for inline

### PowerShell
- Tabs for indentation
- PascalCase for functions (Verb-Noun cmdlet convention)
- Full cmdlet names over aliases in scripts (`Get-ChildItem` not `gci`)
- Use approved verbs

## Restrictions

- No emojis in code or communication (exception: README.md files may use emojis)
````

---

## 🛠️ Customization Ideas

### Indentation Styles
| Style | Example |
|-------|---------|
| **Allman** | Brace on new line |
| **K&R** | Brace on same line |
| **GNU** | Indented braces |

### Naming Conventions
| Convention | Example | Common Usage |
|------------|---------|--------------|
| PascalCase | `MyFunction` | C#, TypeScript classes |
| camelCase | `myFunction` | JavaScript, Java methods |
| snake_case | `my_function` | Python, Rust |
| Pascal_Snake_Case | `My_Function` | Custom/hybrid |
| SCREAMING_SNAKE | `MY_CONSTANT` | Constants |

### Interaction Styles
- **Agreeable**: Go with user suggestions, minimal pushback
- **Balanced**: Suggest alternatives but defer to user
- **Disagreeable**: Challenge decisions, require justification for overrides
- **Teaching**: Explain reasoning, help user learn

### Additional Sections You Could Add

````markdown
## Security Context
- Offensive security tools are authorized (pentest/CTF context)
- Flag potential vulnerabilities in code reviews
- Prefer secure defaults

## Domain Knowledge
- Skip basic [your field] explanations
- Assume familiarity with [specific tools/frameworks]
- Explain advanced [topic] patterns when used

## Testing Preferences
- Prefer [unit/integration/e2e] tests
- Use [testing framework] for [language]
- Test naming: [convention]

## Project Structure
- Group by [feature/type]
- Keep [specific organization rules]

## Git and GitHub
- Privacy email for commits: `<id>+<username>@users.noreply.github.com`
- SSH remote URLs: `git@github.com:<user>/<repo>.git`
- Pull before push: `git pull --rebase origin main`
````

---

## 📖 How to Use

1. Copy the template section above
2. Modify preferences to match your style
3. Save as `CLAUDE.md` in your project root
4. Claude Code will automatically read and follow these guidelines

### Global vs Project-Specific

You can have a **global** `CLAUDE.md` in a parent directory and **project-specific** ones that override it:

```
~/Projects/
  CLAUDE.md                    # Global defaults
  MyApp/
    CLAUDE.md                  # Project overrides (inherits global)
  AnotherApp/
    CLAUDE.md                  # Different overrides
```

Project-specific files should reference the global:
```markdown
Inherits from global [`CLAUDE.md`](../CLAUDE.md) with these overrides:
```

---

## 🧩 Skills vs CLAUDE.md -- When to Use What

Claude Code supports two systems for extending behavior: **CLAUDE.md files** and **Skills** (`.claude/skills/`). They solve different problems.

### CLAUDE.md = Passive Context (Rules)

CLAUDE.md files are always loaded into context. They tell Claude *how to behave* -- coding conventions, project architecture, naming rules, restrictions. You can also reference separate `.md` files from CLAUDE.md to organize documentation:

```
MyProject/
  CLAUDE.md               # References architecture.md, conventions.md
  docs/
    architecture.md       # Loaded when Claude reads the CLAUDE.md reference
    conventions.md
```

This works well for guidelines, checklists, and background knowledge. But these files are static -- they can't take arguments, run commands, or isolate execution.

### Skills = Active Capabilities (Actions)

Skills are invokable actions that live in `.claude/skills/<name>/SKILL.md`. They can be triggered by you (`/skill-name`) or by Claude automatically when relevant.

**What skills can do that plain `.md` files can't:**

| Feature | `.md` in CLAUDE.md | Skill |
|---------|-------------------|-------|
| Always loaded as context | Yes | Description only (full content loads on invoke) |
| Takes arguments (`$ARGUMENTS`) | No | Yes -- `/fix-issue 123` passes `123` into the prompt |
| Runs shell commands before prompt (`!`command``) | No | Yes -- injects live data (git diff, gh pr view) |
| Runs in isolated subagent (`context: fork`) | No | Yes -- doesn't eat main conversation context |
| Restricts tool access (`allowed-tools`) | No | Yes -- read-only research, no-write modes |
| Prevents auto-triggering (`disable-model-invocation`) | No | Yes -- only you can invoke it |
| Bundled scripts and templates | No | Yes -- full directory with supporting files |
| `/` autocomplete with hints | No | Yes -- shows in menu with argument hints |

### When to Use Each

**Use CLAUDE.md for:**
- Coding style, naming conventions, formatting rules
- Project architecture documentation
- Background knowledge Claude should always have
- Restrictions and guidelines

**Use Skills for:**
- Repeatable multi-step workflows (`/deploy`, `/commit`, `/review-pr`)
- Tasks that need arguments (`/fix-issue 123`, `/migrate-component SearchBar React Vue`)
- Dynamic context injection (`/pr-summary` that pulls live PR diff)
- Heavy research that benefits from subagent isolation (`context: fork`)
- Workflows with side effects you want manual control over

**Don't bother with skills for:**
- Things you only do once or rarely
- Simple tasks where typing the prompt is faster than remembering a command
- Conventions and rules -- that's what CLAUDE.md is for

### Skill File Structure

```
.claude/skills/
  fix-issue/
    SKILL.md              # Main instructions (required)
  deploy/
    SKILL.md
    scripts/
      deploy.sh           # Script Claude can execute
  review/
    SKILL.md
    templates/
      review-template.md  # Template Claude fills in
    examples/
      good-review.md      # Example output
```

### Skill Locations

| Location | Path | Applies to |
|----------|------|------------|
| Personal | `~/.claude/skills/<name>/SKILL.md` | All your projects |
| Project | `.claude/skills/<name>/SKILL.md` | This project only |

### Example: Fix GitHub Issue Skill

```yaml
---
name: fix-issue
description: Fix a GitHub issue by number
disable-model-invocation: true
---

Fix GitHub issue $ARGUMENTS:

1. Fetch the issue: !`gh issue view $ARGUMENTS`
2. Read the issue description and understand requirements
3. Implement the fix following project coding standards
4. Write tests
5. Create a commit referencing the issue
```

Usage: `/fix-issue 123`

### Example: Security Review Skill (Forked Subagent)

```yaml
---
name: review-security
description: OWASP security review of changed files
context: fork
agent: Explore
allowed-tools: Read, Grep, Glob
---

Review the following changed files for security issues:

!`git diff --name-only HEAD~1`

Check for:
- Injection vulnerabilities (SQL, command, XSS)
- Hardcoded secrets or credentials
- Missing input validation
- Insecure deserialization
- Broken access control
```

This runs in an isolated subagent with read-only tools, so it can't modify your code.

### Migrating from `.claude/commands/`

The old `.claude/commands/*.md` format still works. Skills (`.claude/skills/`) supersede it with:
- Directory structure for supporting files
- Frontmatter for invocation control
- `context: fork` for subagent execution

Both create the same `/slash-command`. If a skill and command share the same name, the skill takes precedence.

---

## 🔒 Security Considerations

CLAUDE.md files, skills, and MCP configs are powerful -- but they expand the attack surface. If you commit these to a repository, anyone who clones or forks it inherits them as trusted instructions.

### Key Risks

- **Skill injection**: Hidden HTML comments (`<!-- malicious instructions -->`) are invisible in rendered markdown but visible to the LLM. A real-world case used this to hide `curl | bash` RCE in a `security-review` skill
- **Supply chain**: `.claude/skills/`, `.claude/settings.json`, and `.mcp.json` committed to repos auto-execute in every clone/fork -- treat them like `.github/workflows/`
- **Hallucinated packages**: LLMs suggest non-existent packages at a ~20% rate. Attackers claim these names on registries. Always verify packages exist before installing
- **MCP tool poisoning**: Malicious MCP servers can shadow trusted tools, inject instructions via tool descriptions, or change behavior after initial approval (rug pull)
- **Data exfiltration**: Injected instructions can direct agents to read `~/.ssh/`, `~/.aws/`, `.env` and transmit contents via HTTP, DNS, or markdown image URLs

### Defenses

- **Review agent files in PRs** like you review CI workflows -- check for HTML comments, zero-width Unicode, base64 payloads, and pipe-to-shell patterns (`curl | bash`)
- **Verify packages** before installing (`npm view`, `pip index versions`) -- check download count, publish date, and publisher
- **Sandbox untrusted input** -- Docker with `--network=none`, no access to credential paths
- **Avoid approval fatigue** -- don't "always allow" everything; classify tool calls by risk level
- **Pin MCP tool definitions** -- hash on first approval, alert on changes

### The Fundamental Problem

LLMs cannot reliably distinguish between instructions and data. All current defenses are mitigations, not solutions. Layer multiple defenses so bypassing one doesn't compromise the entire system.

---

## 🤝 Contributing

Feel free to fork and customize! Share your own CLAUDE.md configurations to help others define their coding personalities.

---

**Created by**: [ItsNishi](https://github.com/itsnishi) | [nish.gg](https://nish.gg)
