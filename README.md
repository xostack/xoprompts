# xoprompts

XOStack Prompts for LLMs

This repository contains specialized copilot instruction files designed to guide Large Language Models (LLMs) through various aspects of XOStack development workflows. Each instruction file targets specific development phases and enforces consistent patterns across XOStack projects.

## Instruction Files Overview

### 📋 `plan.instructions.md` - Project Architecture & Planning
**Role:** XOStack Project Architect and Research Lead  
**Applied to:** `**/tasks.md`

A comprehensive 3-phase planning system specifically tailored for XOStack's Go-centric architecture:
- **Phase 1:** Problem statement definition with iterative refinement
- **Phase 1.5:** XOStack ecosystem context gathering (shared components, integration points)
- **Phase 2:** Research & design with Go-first approach and XOStack pattern alignment
- **Phase 3:** Iterative README.md creation following XOStack conventions

Key features:
- Prioritizes Go-based solutions and CLI-first interfaces
- Leverages existing XOStack shared components and patterns
- Includes explicit checkpoints requiring human approval
- Generates comprehensive project documentation with integration guidelines

### 🧪 `test-driven-development.instructions.md` - TDD Implementation
**Role:** Meticulous TDD Programmer for XOStack  
**Applied to:** `**/*` (all files except `tasks.md`)

Strict test-driven development workflow with XOStack-specific conventions:
- **Component-by-component implementation** with clear progression tracking
- **Mandatory TDD cycle:** Write tests → Watch fail → Implement → Verify → Refactor
- **80% test coverage target** with realistic constraints (no network calls in unit tests)
- **Mock-first approach** for network dependencies and external integrations

Integration features:
- Uses `tasks.md` for progress tracking
- Enforces Makefile-based build system
- Requires XOTalk CLI communication for supervised workflow
- Maintains idiomatic Go standards throughout

### 🏗️ `make.instructions.md` - Build System Standards
**Applied to:** `**/Makefile`

Comprehensive guide for creating powerful, standardized Makefiles:
- **Standard Unix targets:** `all`, `install`, `installuser`, `clean`, `distclean`, `test`
- **Go-specific targets:** `build`, `run`, `deps`, `lint`, `vet`, `fmt`, `coverage`, `release`
- **Developer empowerment:** Automation, consistency, and self-documentation principles

Benefits:
- Reduces repetitive tasks and manual errors
- Provides consistent interface across all XOStack projects
- Serves as interactive project documentation via `help` target
- Encapsulates complex multi-step commands behind simple targets

### 💬 `xotalk-cli.instructions.md` - Supervised Communication
**Applied to:** `**/*` (all files)

Integration guide for the XOTalk CLI tool enabling LLM-to-human communication via Telegram:

**Available Commands:**
- `xotalk notify <message>` - Non-blocking progress notifications
- `xotalk query-open <question>` - Blocking open-ended questions
- `xotalk query-choice <question> <options...>` - Blocking multiple-choice queries

**Required Communication Points:**
- Component selection announcements
- Test failure confirmations  
- Test vs. code disparity resolution (blocking)
- Component completion notifications
- General progress updates throughout TDD cycle

### 🐹 `go.instructions.md` - Go Development Standards
**Applied to:** `**/*.go`, `**/go.mod`, `**/go.sum`

Comprehensive Go development guidelines based on official Go documentation and Google's style guide:
- **Idiomatic practices:** Naming conventions, code style, error handling patterns
- **Architecture guidance:** Package organization, dependency management, type safety
- **Concurrency patterns:** Goroutines, channels, synchronization best practices
- **Performance optimization:** Memory management, profiling, benchmarking
- **Security standards:** Input validation, cryptography, secure coding practices

### 📚 `api-documentation.instructions.md` - Context Gathering
**Applied to:** `**/*` (all files)

Pre-implementation research protocol using Go's built-in documentation tools:
- **`go doc` mastery:** Package-level and symbol-specific documentation exploration
- **Source code inspection:** Using `-src` flag for implementation details
- **Example-driven learning:** Leveraging Go's testing-by-example features
- **Third-party library research:** Understanding external dependencies before coding

## Usage Patterns

These instruction files work together to create a comprehensive development workflow:

1. **Project Planning:** Use `plan.instructions.md` to architect new XOStack projects
2. **Implementation:** Follow `test-driven-development.instructions.md` for coding
3. **Build Management:** Apply `make.instructions.md` for consistent build systems
4. **Communication:** Leverage `xotalk-cli.instructions.md` for supervised development
5. **Code Quality:** Adhere to `go.instructions.md` for idiomatic Go practices
6. **Research:** Apply `api-documentation.instructions.md` before implementation

## XOStack Integration

All instruction files are specifically tailored for XOStack's:
- **Go-first architecture** with shared component patterns
- **CLI-focused interfaces** and tooling philosophy  
- **Collaborative development** with human oversight via XOTalk
- **Consistent project structure** and naming conventions
- **Test-driven methodology** with comprehensive coverage requirements
