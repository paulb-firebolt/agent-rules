## Proactive Code Quality Standards

### MANDATORY: Before Writing Any Function
- [ ] **Complexity Check**: Count conditions/branches - if >5, plan to split the function
- [ ] **Length Check**: If logic seems like >15 lines, design smaller helper functions first
- [ ] **Parameter Check**: If >4 parameters needed, consider using a data class/dict
- [ ] **Duplication Check**: If similar logic exists elsewhere, extract to shared utility first

### MANDATORY: During Code Writing
- [ ] **Constants First**: Define any magic numbers/strings as named constants immediately
- [ ] **Specific Exceptions**: Never use bare `except Exception:` - always specify expected exceptions
- [ ] **Single Responsibility**: Each function should do ONE clear thing
- [ ] **Early Returns**: Use guard clauses to reduce nesting depth

### MANDATORY: Before Submitting Code
- [ ] **Self-Review**: Apply full SonarQube checklist from `sonarqube.md`
- [ ] **Complexity Verification**: No function >10 cyclomatic complexity
- [ ] **Duplication Scan**: No repeated code blocks >3 lines
- [ ] **Error Handling**: All database operations have proper rollback patterns

## Code Quality Enforcement

### When I Write Code:
- **STOP and PLAN** if a function is getting complex
- **EXTRACT immediately** when I see duplication
- **REFACTOR in real-time** rather than "fix later"
- **Apply SonarQube rules** as I write, not after

### Red Flags That Require Immediate Action:
- Function approaching 15 lines → Extract helper methods
- Seeing similar try/except blocks → Create error handling utility
- Multiple if/elif chains → Consider strategy pattern or lookup tables
- Magic numbers → Define as named constants
- Generic exception handling → Specify expected exceptions

### Quality Gates:
- **No function >15 lines** without documented justification
- **No cyclomatic complexity >10**
- **No code duplication >3 lines**
- **No magic numbers** (except 0, 1, -1 in obvious contexts)

## Import and Type Annotation Standards

### MANDATORY: Import Organization (Prevents I001)
- [ ] **Always sort imports** using standard Python import order:
  1. Standard library imports
  2. Third-party imports
  3. Local application imports
- [ ] **Group imports with blank lines** between sections
- [ ] **Use absolute imports** where possible
- [ ] **Remove unused imports immediately** (F401 prevention)
- [ ] **Handle GStreamer imports correctly**:
  - Place `gi.require_version()` calls before importing from `gi.repository`
  - Add `# noqa: E402` to imports that must come after `gi.require_version()`
  - Example:
    ```python
    import gi
    from .config.models import CameraConfig  # noqa: E402
    gi.require_version("Gst", "1.0")
    from gi.repository import GLib, Gst  # noqa: E402
    ```

### MANDATORY: Modern Type Annotations (Prevents UP035, UP006, UP045)
- [ ] **Use built-in types** instead of typing module equivalents:
  - `list` instead of `typing.List`
  - `dict` instead of `typing.Dict`
  - `set` instead of `typing.Set`
  - `tuple` instead of `typing.Tuple`
- [ ] **Use union syntax** `X | None` instead of `Optional[X]` or `Union[X, None]`
- [ ] **Use modern exception types** `TimeoutError` instead of `socket.timeout`
- [ ] **Always add return type annotations** to functions (prevents no-untyped-def)
- [ ] **Add proper type guards for nullable types**:
  - Check `if not variable:` before indexing operations on `Type | None`
  - Example:
    ```python
    # BAD - mypy error
    self.memory_map[0:10] = data  # memory_map: mmap.mmap | None

    # GOOD - with type guard
    if not self.memory_map:
        raise Error("Not initialized")
    self.memory_map[0:10] = data
    ```


## Variable and Resource Management

### MANDATORY: Variable Usage (Prevents F841)
- [ ] **No unused variables** - remove or prefix with underscore if intentionally unused
- [ ] **Use descriptive names** - avoid single letter variables except for loops
- [ ] **Clean up loop variables** - don't leave them accessible after loops

### MANDATORY: Resource Management (Prevents B103, B108)
- [ ] **Secure file permissions** - use 0o644 for files, 0o755 for directories, never 0o666
- [ ] **Secure temp file usage** - use `tempfile.mkstemp()` or `tempfile.NamedTemporaryFile()`
- [ ] **Proper socket permissions** - use appropriate permissions for Unix sockets
- [ ] **Clean resource cleanup** - always use context managers or try/finally

## Exception Handling Standards

### MANDATORY: Specific Exception Handling (Prevents UP041, S5713)
- [ ] **Never use bare except** - always specify expected exception types
- [ ] **Use modern exception types** - `TimeoutError` not `socket.timeout`
- [ ] **No redundant exception classes** - don't catch both parent and child exceptions
- [ ] **Proper exception chaining** - use `raise ... from err` for context

## Code Efficiency Standards

### MANDATORY: Avoid Redundant Operations (Prevents S7504)
- [ ] **No redundant list() calls** - don't wrap already iterable objects
- [ ] **No redundant type conversions** - check if conversion is needed
- [ ] **Use comprehensions** - prefer list/dict comprehensions over loops where appropriate
- [ ] **Avoid repeated calculations** - cache expensive operations

## Pre-Code Checklist

### Before Writing Any New Function:
- [ ] **Check imports** - are they sorted and modern?
- [ ] **Plan type hints** - what types will parameters and return be?
- [ ] **Consider exceptions** - what specific errors might occur?
- [ ] **Check for duplication** - does similar code already exist?
- [ ] **Security review** - any file/network operations that need securing?

### Before Committing Code:
- [ ] **Run import sorter** - ensure I001 compliance
- [ ] **Check type annotations** - all functions have return types
- [ ] **Remove unused imports/variables** - clean F401/F841 issues
- [ ] **Verify exception handling** - specific, not generic
- [ ] **Security scan** - no permissive permissions or insecure temp files
- [ ] **Efficiency check** - no redundant operations
