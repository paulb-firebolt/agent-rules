# Agent Rules

This is a simple list of rules that I first created whilst using the VSCode extension Cline.

The files ended up un ~/Documents/Client/Rules, I decided to leave them there and in other projects make reference to them so I have a consistent approach to agent coding.

For CLAUDE.md and AGENT.md files in my projects I simply reference the rules like this:

```markdown
# Agent Instructions

This project is used to scan systems for vulnerabilities and record findings.

## Coding Practices

- Do no use any deprecated features like Optional, or List
- Use strict typing where possible

## Other Rules

See rules under ~/Documents/Cline/Rules
```

This seems sufficient to have the agent follow my instructions.

Yet to be tested with gemini.
