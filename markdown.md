# Markdown Writing Standards for Agents

When writing or editing markdown documentation, follow these rules to comply with our markdownlint configuration:

## Document Structure (MD025 - Multiple top-level headings)
- **Use only ONE `#` (H1) heading per document** - this should be the document title
- Use `##` (H2) for major sections, `###` (H3) for subsections, etc.
- If you need to reference the project name or create emphasis, use `##` instead of another `#`

### Frontmatter and MD025 Issues
- **When documents have YAML frontmatter with a `title:` field, markdownlint may treat it as a heading**
- If you have frontmatter with a title AND an H1 heading, add this comment after the frontmatter:

```markdown
---
title: Potential Metrics Analysis - What Services Could Provide
created: 2025-01-17T15:47:00Z
updated: 2025-01-17T15:47:00Z
---

<!-- markdownlint-disable MD025 -->

# Potential Metrics Analysis - What Services Could Provide

## Overview
Content here...
```

Example without frontmatter:
```markdown
# Health Monitoring Implementation Guide

## Overview
Content here...

## Configuration
Content here...

## Troubleshooting
Content here...
```

## Code Blocks (MD040 - Fenced code blocks should have language)
- **Always specify a language for fenced code blocks**
- Use appropriate language identifiers:
  - `python` - For Python code
  - `bash` or `shell` - For command line examples
  - `json` - For JSON configuration
  - `yaml` - For YAML files
  - `sql` - For database queries
  - `text` - For plain text output, logs, or generic content
  - `console` - For command line sessions with prompts
  - `http` - For HTTP requests/responses
  - `diff` - For showing differences

Example:

Run the following command:

```bash
python manage.py migrate
```

The output will look like this:

```text
Operations to perform:
  Apply all migrations: auth, contenttypes
Running migrations:
  Applying auth.0001_initial... OK
```

```text
## URLs (MD034 - Bare URL used)
- **Always wrap URLs in angle brackets `<>` or use proper markdown links**
- Don't paste raw URLs directly in text

Instead of:
```markdown
Visit https://example.com for more info
```

Use:
```markdown
Visit <https://example.com> for more info
```

Or:
```markdown
Visit [our documentation](https://example.com) for more info
```

## Headings vs Emphasis (MD036 - Emphasis used instead of heading)
- **Use proper headings (`##`, `###`, etc.) instead of bold/italic for section titles**
- Reserve `**bold**` and `*italic*` for emphasis within sentences, not as pseudo-headings

Instead of:
```markdown
**Configuration Steps**

Here are the steps...
```

Use:
```markdown
## Configuration Steps

Here are the steps...
```

## Duplicate Headings (MD024 - Multiple headings with same content)
- **Make heading text unique within the document**
- Add context or numbering to distinguish similar sections
- **Never use emojis in headings** - they can cause duplicate content issues and reduce readability

Instead of:
```markdown
## Implementation

...

## Implementation
```

Use:
```markdown
## Initial Implementation

...

## Final Implementation
```

Or:
```markdown
## Implementation - Phase 1
...
## Implementation - Phase 2
```

## List Formatting - MkDocs Compatibility
- **Always add a blank line before lists** - MkDocs requires this for proper rendering
- This applies to both numbered lists and bulleted lists

Instead of:
```markdown
Here are the steps:
1. First step
2. Second step
```

Use:
```markdown
Here are the steps:

1. First step
2. Second step
```

Instead of:
```markdown
Key points:
- Point one
- Point two
```

Use:
```markdown
Key points:

- Point one
- Point two
```

## Emoji Usage - AVOID IN DOCUMENTATION
- **Do NOT use emojis in headings, titles, or professional documentation**
- Emojis can cause duplicate heading issues when markdownlint strips them for comparison
- They reduce accessibility and professional appearance
- They can cause encoding issues in different systems

Instead of:
```markdown
## 🚀 Implementation
## 📊 Metrics Analysis
## ✅ Results
```

Use:
```markdown
## Implementation
## Metrics Analysis
## Results
```

## Quick Checklist for Claude
When writing markdown documentation:
- [ ] Only one `#` heading in the entire document
- [ ] If frontmatter contains `title:` field, add `<!-- markdownlint-disable MD025 -->` after frontmatter
- [ ] All code blocks have language specified (use `text` if unsure)
- [ ] URLs are wrapped in `<>` or proper markdown links
- [ ] Bold/italic used for emphasis, not as headings
- [ ] All headings have unique text within the document
- [ ] Structure uses proper heading hierarchy (`#` > `##` > `###`)
- [ ] **NO EMOJIS** in headings, titles, or professional documentation
- [ ] **Blank line before all lists** (required for MkDocs rendering)

## Common Language Identifiers Reference
- `python`, `javascript`, `typescript`, `java`, `go`, `rust`
- `bash`, `shell`, `powershell`, `cmd`
- `json`, `yaml`, `xml`, `toml`, `ini`
- `sql`, `dockerfile`, `nginx`
- `html`, `css`, `markdown`
- `text` - Use this for plain text, logs, output, or when unsure
- `console` - For command line sessions
- `http` - For API examples
- `diff` - For showing changes
