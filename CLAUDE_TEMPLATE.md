# CLAUDE.md Template

A customizable configuration file for [Claude Code](https://claude.ai/code) to define your coding personality and preferences.

---

## 🎯 What is This?

This file tells Claude Code how you like to work. Drop it in your project root and Claude will follow your coding style, communication preferences, and conventions automatically.

## 📋 Template

```markdown
# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 🔧 Code Style

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

## 💬 Interaction Style

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

## 🖥️ Language-Specific Preferences

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

### PowerShell
- Tabs for indentation
- PascalCase for functions (Verb-Noun cmdlet convention)
- Full cmdlet names over aliases in scripts (`Get-ChildItem` not `gci`)
- Use approved verbs

## 🚫 Restrictions

- No emojis in code or communication
```

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

```markdown
## 🔐 Security Context
- Offensive security tools are authorized (pentest/CTF context)
- Flag potential vulnerabilities in code reviews
- Prefer secure defaults

## 📚 Domain Knowledge
- Skip basic [your field] explanations
- Assume familiarity with [specific tools/frameworks]
- Explain advanced [topic] patterns when used

## 🧪 Testing Preferences
- Prefer [unit/integration/e2e] tests
- Use [testing framework] for [language]
- Test naming: [convention]

## 📁 Project Structure
- One class per file
- Group by [feature/type]
- Keep [specific organization rules]
```

---

## 📖 How to Use

1. Copy the template section above
2. Modify preferences to match your style
3. Save as `CLAUDE.md` in your project root
4. Claude Code will automatically read and follow these guidelines

---

## 🤝 Contributing

Feel free to fork and customize! Share your own CLAUDE.md configurations to help others define their coding personalities.

---

**Created by**: [ItsNishi](https://github.com/itsnishi) | [nish.gg](https://nish.gg)
