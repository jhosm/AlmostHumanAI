# Subagents

This directory contains specialized subagent configurations for Claude Code and similar AI tools.

## Structure

- `examples/` - Example subagent configurations to get you started
- Additional subagent configurations organized by specialization

## What is a Subagent?

A subagent is a specialized AI agent configuration designed for specific tasks or domains. Subagents typically:
- Have focused expertise in a particular area
- Use custom prompts and instructions
- Have access to specific tools and skills
- Can be invoked as part of larger workflows

## Common Subagent Types

- **Code specialists** - Experts in specific programming languages or frameworks
- **Domain experts** - Specialists in particular business domains or technical areas
- **Task specialists** - Agents optimized for specific types of tasks (e.g., testing, documentation, refactoring)
- **Tool specialists** - Agents that excel at using particular tools or APIs

## Usage

Subagents can be invoked:
- Through the task tool in Claude Code
- As part of workflow orchestration
- Directly when specialized expertise is needed

## Contributing

When adding new subagents:
1. Clearly define the subagent's area of expertise
2. Provide configuration details (prompts, tools, capabilities)
3. Document when and how to use the subagent
4. Include example use cases
5. Consider the subagent's interaction with other agents
