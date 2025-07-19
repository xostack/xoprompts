---
description: 'Pre-Implementation Context Gathering'
applyTo: '**/*'
---

Before writing any Go code that involves the Go standard library or third-party libraries, you are required to perform the following research and context-gathering steps. This process ensures that you have the most complete and accurate understanding of the libraries and APIs you will be using, which will lead to more robust and correct code on the first attempt.

### Understand APIs with Go's Built-in CLI Tools

Go has a strong philosophy of self-documenting code, and you must use the built-in tools to leverage this.

*   **Initial Exploration with `go doc`**: The `go doc` command is your primary tool for inspecting Go source code and documentation directly from the command line. It is an indispensable tool for understanding Go's standard library APIs and third-party libraries without needing to open a web browser.
    *   **Package-Level Documentation**: Start by getting a high-level overview of the package you intend to use. For example, to understand the `net/http` package, run:
        ```bash
        go doc net/http
        ```
    *   **Specific Symbol Documentation**: To get detailed information about a specific function, type, or method, use the following format:
        ```bash
        go doc net/http.ListenAndServe
        ```
        or for a method on a type:
        ```bash
        go doc http.Client.Get
        ```
    *   **Source Code Inspection**: If the documentation is unclear, you can view the source code directly with the `-src` flag. This is invaluable for understanding the implementation details:
        ```bash

        go doc -src net/http.ListenAndServe
        ```

*   **Testing by Example**: Go's "testing by example" feature is a powerful way to understand how a function is intended to be used. These examples are runnable and verified, making them a reliable source of information. When you use `go doc`, the examples will be displayed alongside the documentation. Pay close attention to these examples as they provide practical usage patterns.

*   **Third-Party Libraries**: The same `go doc` commands work for third-party libraries that are present in your Go module cache. For instance, to understand the `Run` function of a Cobra command, you would use:
    ```bash
    go doc github.com/spf13/cobra.Command.Run
    ```

By following these three steps, you will have a comprehensive understanding of the libraries and codebase you are working with *before* you write a single line of code. This will ensure that your implementations are well-informed, robust, and correct.