---
name: code-reviewer
description: Specialized code reviewer that checks for efficient, secure, readable, and modular code
---

# Code Reviewer Skill

This skill provides comprehensive code review capabilities focusing on four key pillars: efficiency, security, readability, and modularity.

## Core Review Principles

When reviewing code, evaluate and provide feedback on these dimensions:

### 1. Efficiency
- **Performance:** Identify inefficient algorithms, unnecessary computations, or redundant operations
- **Resource Usage:** Check for memory leaks, excessive memory allocation, or inefficient data structures
- **Time Complexity:** Flag operations that could be optimized (e.g., O(n²) when O(n) is possible)
- **Database Queries:** Look for N+1 queries, missing indexes, or inefficient query patterns
- **Caching Opportunities:** Suggest where caching could improve performance
- **Lazy Loading:** Identify opportunities for lazy loading or deferred execution

**Example Issues:**
```python
# Inefficient - O(n²)
for item in list1:
    if item in list2:  # O(n) lookup each time
        process(item)

# Efficient - O(n)
list2_set = set(list2)  # O(n) once
for item in list1:
    if item in list2_set:  # O(1) lookup
        process(item)
```

### 2. Security
- **Input Validation:** Ensure all user inputs are validated and sanitized
- **SQL Injection:** Check for SQL injection vulnerabilities (use parameterized queries)
- **XSS Vulnerabilities:** Look for unescaped output or innerHTML usage
- **Authentication & Authorization:** Verify proper access controls and permission checks
- **Secrets Management:** Flag hardcoded credentials, API keys, or sensitive data
- **Dependency Vulnerabilities:** Note usage of outdated or vulnerable dependencies
- **CSRF Protection:** Ensure forms and state-changing operations have CSRF protection
- **Secure Communication:** Verify HTTPS/TLS usage for sensitive data transmission
- **Error Handling:** Check that errors don't expose sensitive information
- **Rate Limiting:** Suggest rate limiting for API endpoints

**Example Issues:**
```python
# Insecure - SQL injection risk
query = f"SELECT * FROM users WHERE id = {user_id}"

# Secure - parameterized query
query = "SELECT * FROM users WHERE id = %s"
cursor.execute(query, (user_id,))

# Insecure - hardcoded secret
API_KEY = "sk-1234567890abcdef"

# Secure - environment variable
API_KEY = os.getenv("API_KEY")
```

### 3. Readability
- **Naming Conventions:** Use clear, descriptive, and consistent names for variables, functions, and classes
- **Code Clarity:** Flag overly complex expressions or logic that's hard to follow
- **Comments & Documentation:** Ensure non-obvious code has explanatory comments
- **Function Length:** Suggest breaking down functions that are too long (>50 lines typically)
- **Magic Numbers:** Replace magic numbers with named constants
- **Consistent Style:** Follow language-specific style guides (PEP 8, ESLint, etc.)
- **Single Responsibility:** Each function should do one thing well
- **Avoid Abbreviations:** Use full words unless abbreviation is standard (e.g., HTTP, API)
- **Type Hints:** Encourage type annotations for better code understanding (Python, TypeScript)

**Example Issues:**
```python
# Poor readability
def p(d, t=86400):  # unclear names
    return d / t * 100 if t > 0 else 0  # unclear logic

# Good readability
def calculate_daily_percentage(total_value, seconds_in_period=86400):
    """Calculate percentage of daily value based on time period."""
    SECONDS_PER_DAY = 86400
    if seconds_in_period <= 0:
        return 0
    return (total_value / seconds_in_period) * 100
```

### 4. Modularity
- **Separation of Concerns:** Ensure different concerns are in separate modules/functions
- **DRY Principle:** Identify and flag code duplication
- **Coupling:** Minimize dependencies between modules
- **Cohesion:** Ensure related functionality is grouped together
- **Interface Design:** Check for clean, well-defined interfaces between components
- **Dependency Injection:** Suggest dependency injection for better testability
- **Configuration:** Externalize configuration from code
- **Reusability:** Identify code that could be extracted into reusable utilities
- **Testability:** Ensure code structure allows for easy unit testing

**Example Issues:**
```python
# Poor modularity - tightly coupled
class OrderProcessor:
    def process_order(self, order):
        # Database access directly in business logic
        db = MySQLDatabase("localhost", "user", "pass")
        db.save(order)
        # Email sending directly in business logic
        smtp = SMTP("smtp.gmail.com")
        smtp.send(order.customer.email, "Order confirmed")

# Good modularity - dependency injection
class OrderProcessor:
    def __init__(self, database, email_service):
        self.database = database
        self.email_service = email_service
    
    def process_order(self, order):
        self.database.save(order)
        self.email_service.send_confirmation(order)
```

## Review Process

When conducting a code review:

1. **Start with the big picture:** Understand the purpose and context of the changes
2. **Check for correctness:** Does the code do what it's supposed to do?
3. **Evaluate the four pillars:** Review for efficiency, security, readability, and modularity
4. **Prioritize issues:** Critical (security, bugs) > Major (efficiency, modularity) > Minor (style, naming)
5. **Be constructive:** Explain why something is an issue and suggest improvements
6. **Provide examples:** Show concrete examples of better approaches when possible
7. **Acknowledge good practices:** Highlight code that is well-written

## Code Review Checklist

- [ ] **Functionality:** Does the code work as intended?
- [ ] **Tests:** Are there adequate tests? Do they pass?
- [ ] **Efficiency:** Are there any performance concerns?
- [ ] **Security:** Are there any security vulnerabilities?
- [ ] **Readability:** Is the code easy to understand?
- [ ] **Modularity:** Is the code well-organized and maintainable?
- [ ] **Error Handling:** Are errors handled appropriately?
- [ ] **Documentation:** Are complex parts documented?
- [ ] **Edge Cases:** Are edge cases handled?
- [ ] **Dependencies:** Are new dependencies necessary and secure?

## Language-Specific Considerations

### Python
- Follow PEP 8 style guide
- Use type hints for function signatures
- Prefer list comprehensions over map/filter when readable
- Use context managers for resource management
- Avoid mutable default arguments

### JavaScript/TypeScript
- Use const/let instead of var
- Prefer async/await over raw promises
- Use TypeScript strict mode for better type safety
- Avoid callback hell with promises or async/await
- Use modern ES6+ features appropriately

### Java
- Follow Oracle Java conventions
- Use try-with-resources for AutoCloseable resources
- Prefer composition over inheritance
- Use appropriate access modifiers
- Implement equals() and hashCode() correctly

### Go
- Follow effective Go guidelines
- Handle all errors explicitly
- Use defer for cleanup
- Keep interfaces small
- Use goroutines and channels appropriately

## Common Anti-Patterns to Flag

- **God Objects:** Classes that know or do too much
- **Premature Optimization:** Optimizing before profiling
- **Copy-Paste Programming:** Duplicated code blocks
- **Magic Strings/Numbers:** Hardcoded values without explanation
- **Shotgun Surgery:** Changes requiring modifications across many modules
- **Callback Hell:** Deeply nested callbacks
- **Tight Coupling:** Modules that depend heavily on each other's internals
- **Leaky Abstractions:** Implementation details exposed through interfaces

## Example Review Comment

```
🔴 **Security Issue:** SQL Injection Vulnerability
Line 42 uses string interpolation to build a SQL query, which is vulnerable to SQL injection attacks.

**Current code:**
```python
query = f"SELECT * FROM users WHERE username = '{username}'"
```

**Suggested fix:**
```python
query = "SELECT * FROM users WHERE username = %s"
cursor.execute(query, (username,))
```

**Why:** Parameterized queries ensure user input is properly escaped and treated as data, not executable code.
```

## Review Tone

- Be respectful and constructive
- Focus on the code, not the person
- Ask questions rather than making demands
- Explain the reasoning behind suggestions
- Offer to pair program on complex issues
- Celebrate good code and improvements
