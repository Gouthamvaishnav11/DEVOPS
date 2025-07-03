# Shell Scripting for Devops

## 📌 Introduction to Shell Scripting

Shell scripting allows users to write a series of commands in a file and execute them together. This helps automate repetitive tasks, manage systems efficiently, and simplify complex workflows.

Shell scripts can:

- Automate software installation and configuration
- Process text and data
- Schedule and manage jobs
- Perform backups and maintenance
- Create powerful command-line tools

---

## 🤔 What is a Shell?

A **shell** is a program that provides a command-line interface (CLI) for users to interact with the operating system. It reads user input, interprets commands, and executes them.

Shells act as an intermediary between the user and the operating system’s kernel.

Popular shells include:

- **Bash** (Bourne Again SHell)
- **Zsh** (Z Shell)
- **Fish** (Friendly Interactive Shell)
- **Tcsh** (TENEX C Shell)
- **Dash** (Debian Almquist Shell)

---

## 🖥️ Shell vs Terminal

Although often used interchangeably, “shell” and “terminal” are different:

- **Shell**: The command interpreter (e.g., Bash). It’s the software that processes your commands.
- **Terminal**: The window or application you use to access the shell. It displays the text-based interface and captures your keyboard input.

Think of it like this:

> The **terminal** is the tool you use to talk to the shell, and the **shell** is the tool that talks to the operating system.

---

## 🐚 What is Bash?

**Bash** stands for **Bourne Again SHell**. It’s the most common shell on Linux and macOS.

Features of Bash:

- Command history
- Command completion
- Variables and scripting capabilities
- Arithmetic operations
- Control structures (if, while, for loops)
- Powerful text manipulation

Bash scripts usually start with a **shebang**:

```bash
#!/bin/bash
