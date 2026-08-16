# ALIAS in Linux

## Real-Life Use Case

Linux commands can be long and repetitive. **Aliases** let you create short, easy-to-remember names for frequently used commands, saving time and reducing typing errors.

### Examples

- Replace `ls -lah` with `ll`
- Replace `docker ps -a` with `dps`
- Replace `kubectl` with `k`
- Replace `terraform` with `tf`

---

## What is an Alias in Linux?

An **alias** is a custom shortcut for a Linux command or a group of commands. Instead of typing a long command repeatedly, you can assign it a short name and execute it quickly.

Aliases are commonly used by Linux administrators, DevOps engineers, and developers to improve command-line productivity.

---

## Linux Alias Syntax

### Syntax

```bash
alias alias_name='command'
```

---

## Create an Alias

Create an alias for `ls -lah`:

```bash
alias ll='ls -lah'
```

Now simply run:

```bash
ll
```

The shell executes:

```bash
ls -lah
```

---

## Create Multiple Aliases

You can create multiple aliases:

```bash
alias cls='clear'
alias h='history'
alias c='cd'
```

Examples:

```bash
cls
h
c /var/log
```

---

## Alias with Multiple Commands

Aliases can execute multiple commands:

```bash
alias update='sudo apt update && sudo apt upgrade -y'
```

Running:

```bash
update
```

executes both commands sequentially.

---

## View All Aliases

Display all currently configured aliases:

```bash
alias
```

---

## View a Specific Alias

Check how a specific alias is configured:

```bash
alias ll
```

Example output:

```text
alias ll='ls -lah'
```

---

## Remove an Alias

Use the **`unalias`** command:

```bash
unalias ll
```

Verify:

```bash
alias ll
```

If the alias has been removed, the shell will report that the alias does not exist.

### Remove All Aliases

```bash
unalias -a
```

> **Warning:** This removes all aliases from the current shell session.

---

## Create Permanent Aliases

Aliases created directly in the terminal are temporary. They disappear when the shell session ends.

To make aliases permanent, add them to your shell configuration file.

### Bash

Edit:

```bash
nano ~/.bashrc
```

Add:

```bash
alias ll='ls -lah'
alias cls='clear'
alias update='sudo apt update && sudo apt upgrade -y'
```

Reload the configuration:

```bash
source ~/.bashrc
```

The aliases are now available in new Bash sessions.

### Zsh

For Zsh, edit:

```bash
nano ~/.zshrc
```

Add your aliases and reload:

```bash
source ~/.zshrc
```

---

## Common DevOps Aliases

### Docker

```bash
alias d='docker'
alias dps='docker ps'
alias dpsa='docker ps -a'
```

### Docker Compose

```bash
alias dc='docker compose'
alias dcu='docker compose up'
alias dcd='docker compose down'
```

### Kubernetes

```bash
alias k='kubectl'
alias kgp='kubectl get pods'
alias kgs='kubectl get services'
```

### Terraform

```bash
alias tf='terraform'
alias tfi='terraform init'
alias tfp='terraform plan'
alias tfa='terraform apply'
```

### Git

```bash
alias gs='git status'
alias gp='git pull'
alias gps='git push'
alias gl='git log --oneline'
```

These aliases can significantly reduce typing for frequently used DevOps commands.

---

## Alias vs Function

Aliases are useful for simple command shortcuts:

```bash
alias ll='ls -lah'
```

For more complex commands that require arguments or logic, **shell functions** are usually better.

Example:

```bash
mkcd() {
    mkdir -p "$1" && cd "$1"
}
```

Now:

```bash
mkcd projects
```

creates the directory and changes into it.

> **Rule of thumb:** Use an **alias** for simple substitutions and a **function** when you need arguments, logic, or multiple steps.

---

## Check Whether a Command is an Alias

Use:

```bash
type ll
```

Example:

```text
ll is aliased to `ls -lah'
```

You can also use:

```bash
type -a ls
```

This helps determine whether a command is an alias, function, builtin, or executable.

---

## Benefits of Using Aliases

- Reduces typing of long commands
- Increases command-line productivity
- Minimizes typing errors
- Simplifies frequently used commands
- Speeds up daily administration tasks
- Improves workflows for Linux, DevOps, and Cloud engineers
- Makes frequently used commands easier to remember

---

## Best Practices

- Use short and meaningful alias names.
- Store permanent aliases in `~/.bashrc` or `~/.zshrc`.
- Avoid overriding important Linux commands such as `rm`, `cp`, or `mv` unless intentional.
- Group related aliases together.
- Use comments to document complex aliases.
- Use functions instead of aliases when arguments or logic are required.
- Keep your aliases consistent across development environments.

---

## Why Learn Aliases?

Aliases are one of the easiest ways to improve productivity in Linux. They eliminate repetitive typing, simplify frequently used commands, and make daily tasks faster.

Whether you're managing servers or working with **Git, Docker, Kubernetes, Terraform, or AWS**, aliases can help you work more efficiently from the command line.

---

## Quick Reference

```bash
# Create an alias
alias ll='ls -lah'

# Run the alias
ll

# View all aliases
alias

# View a specific alias
alias ll

# Remove an alias
unalias ll

# Remove all aliases
unalias -a

# Check what a command is
type ll

# Make aliases permanent in Bash
nano ~/.bashrc

# Reload Bash configuration
source ~/.bashrc
```
