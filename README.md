# AlmostHumanAI

A collection of specialized GitHub Copilot Agent Skills for enhanced AI-assisted development.

## Skills

### Code Reviewer

A comprehensive code review skill that evaluates code across four key dimensions:

- **Efficiency**: Identifies performance bottlenecks, inefficient algorithms, and optimization opportunities
- **Security**: Detects vulnerabilities like SQL injection, XSS, hardcoded secrets, and authentication issues
- **Readability**: Ensures code is clean, well-named, properly documented, and follows style guidelines
- **Modularity**: Promotes DRY principles, loose coupling, high cohesion, and testable code architecture

**Location**: `.github/skills/code-reviewer/`

**Usage**: This skill is automatically available to GitHub Copilot when working in this repository. The AI assistant will use these guidelines when performing code reviews or providing suggestions.

### Features

- Language-specific best practices for Python, JavaScript/TypeScript, Java, and Go
- Common anti-pattern detection
- Security vulnerability identification
- Performance optimization suggestions
- Code maintainability improvements
- Concrete before/after examples

## Installation

To use these skills:

1. Ensure you have GitHub Copilot enabled in your IDE (VS Code, JetBrains, etc.)
2. Clone this repository or copy the `.github/skills/` directory to your project
3. For global skills, copy to `~/.copilot/skills/`
4. The skills will be automatically detected by GitHub Copilot

## Contributing

Feel free to submit pull requests to improve existing skills or add new ones!

## License

See [LICENSE](LICENSE) file for details.