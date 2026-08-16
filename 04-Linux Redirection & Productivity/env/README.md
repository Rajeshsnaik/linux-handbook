# Set Environment Variables in Linux

## What are Environment Variables?

**Environment variables** are key-value pairs used by the operating system and applications to store configuration settings. They allow programs and scripts to access information such as user details, file paths, shell settings, and application-specific configurations.

### Examples

- `PATH`
- `HOME`
- `USER`
- `HOSTNAME`
- `JAVA_HOME`
- `AWS_REGION`

---

## View All Environment Variables

Display all environment variables:

```bash
printenv
```

or:

```bash
env
```

---

## View a Specific Environment Variable

Display the value of a variable:

```bash
echo $HOME
```

Another example:

```bash
echo $PATH
```

---

## Create a Temporary Environment Variable

Use the **`export`** command:

```bash
export APP_NAME="MyApp"
```

Verify it:

```bash
echo $APP_NAME
```

> **Note:** Temporary environment variables exist only for the current shell session. They are lost when the shell exits.

---

## Create a Permanent Environment Variable

To make a variable available whenever you start a shell, add it to your shell configuration file.

### Bash

Edit `~/.bashrc`:

```bash
nano ~/.bashrc
```

Add:

```bash
export APP_NAME="MyApp"
```

Reload the configuration:

```bash
source ~/.bashrc
```

Verify:

```bash
echo $APP_NAME
```

---

## Add a Directory to PATH

The `PATH` variable tells Linux where to look for executable programs.

```bash
export PATH=$PATH:/opt/scripts
```

Verify:

```bash
echo $PATH
```

> **Tip:** When adding directories to `PATH`, avoid overwriting the existing value. Use `$PATH` to preserve the current directories.

---

## Set JAVA_HOME

Example for a Java installation:

```bash
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk
```

Update `PATH`:

```bash
export PATH=$JAVA_HOME/bin:$PATH
```

For a permanent configuration, add these lines to `~/.bashrc`:

```bash
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk
export PATH=$JAVA_HOME/bin:$PATH
```

---

## Set AWS Environment Variables

AWS CLI and SDKs can use environment variables for configuration.

```bash
export AWS_ACCESS_KEY_ID=YOUR_ACCESS_KEY
export AWS_SECRET_ACCESS_KEY=YOUR_SECRET_KEY
export AWS_DEFAULT_REGION=ap-south-1
```

> **Security Warning:** Avoid storing AWS access keys directly in shell configuration files such as `~/.bashrc`. For AWS workloads, prefer IAM roles, AWS credential profiles, or other secure credential-management methods.

---

## Remove an Environment Variable

Use the **`unset`** command:

```bash
unset APP_NAME
```

Verify:

```bash
echo $APP_NAME
```

No value will be displayed.

---

## Check Shell Configuration Files

Different shells use different configuration files.

| Shell / Scope | Configuration File |
| ------------- | ------------------ |
| Bash          | `~/.bashrc`        |
| Bash Login    | `~/.bash_profile`  |
| Zsh           | `~/.zshrc`         |
| System-wide   | `/etc/environment` |
| Global Bash   | `/etc/profile`     |

> **Note:** The exact file loaded depends on whether the shell is interactive, login-based, or non-interactive.

---

## System-Wide Environment Variables

To make environment variables available system-wide, edit:

```bash
sudo nano /etc/environment
```

Example:

```text
APP_NAME="MyApp"
JAVA_HOME="/usr/lib/jvm/java-17-openjdk"
```

Log out and log back in for the changes to take effect.

> **Important:** `/etc/environment` uses `KEY=VALUE` syntax. Do **not** use the `export` keyword in this file.

---

## Check if a Variable Exists

Use:

```bash
printenv APP_NAME
```

or:

```bash
echo $APP_NAME
```

A more reliable check is:

```bash
if [ -n "$APP_NAME" ]; then
    echo "APP_NAME is set"
else
    echo "APP_NAME is not set"
fi
```

---

## Common Environment Variables

| Variable     | Description                                  |
| ------------ | -------------------------------------------- |
| `PATH`       | Directories searched for executable commands |
| `HOME`       | User's home directory                        |
| `USER`       | Current logged-in user                       |
| `PWD`        | Current working directory                    |
| `HOSTNAME`   | System hostname                              |
| `SHELL`      | Current shell                                |
| `JAVA_HOME`  | Java installation path                       |
| `AWS_REGION` | Default AWS region                           |

---

## Common Use Cases

Environment variables are commonly used to:

- Configure Java using `JAVA_HOME`
- Set Python or Node.js paths
- Configure AWS CLI and SDKs
- Add custom scripts to `PATH`
- Store application configuration
- Pass configuration to Docker containers
- Configure Kubernetes workloads
- Configure CI/CD pipelines
- Manage application runtime settings

---

## Best Practices

- Use `export` for variables that child processes need to access.
- Store user-specific variables in `~/.bashrc` or `~/.zshrc` when appropriate.
- Use `/etc/environment` for simple system-wide variables.
- Use `/etc/profile.d/` for maintainable system-wide shell configuration.
- Avoid storing sensitive credentials in plain-text shell configuration files.
- Prefer IAM roles and secure credential mechanisms for AWS workloads.
- Preserve the existing `PATH` when adding new directories.
- Verify environment variables using `printenv`, `env`, or `echo`.

---

## Why Learn Environment Variables?

Environment variables are essential for configuring Linux systems and applications. They are widely used in:

- Linux Administration
- Shell Scripting
- DevOps
- Cloud Computing
- Docker
- Kubernetes
- CI/CD Pipelines
- Software Development
- System Administration

They allow applications to access configuration and runtime settings **without modifying application source code**.

---

# Set Permanent Environment Variables for All Users

To make an environment variable available to **all users** on a Linux system, define it in a **system-wide configuration file**. These changes generally require **root (`sudo`) privileges**.

---

## Method 1: `/etc/environment`

`/etc/environment` is a simple system-wide configuration file for environment variables.

Edit the file:

```bash
sudo nano /etc/environment
```

Add variables:

```text
APP_NAME="MyApp"
JAVA_HOME="/usr/lib/jvm/java-17-openjdk"
```

Log out and log back in for the changes to take effect.

### Important

`/etc/environment` does **not** use shell syntax.

Correct:

```text
APP_NAME="MyApp"
```

Incorrect:

```bash
export APP_NAME="MyApp"
```

---

## Method 2: `/etc/profile`

`/etc/profile` is used for system-wide settings in login shells.

Edit the file:

```bash
sudo nano /etc/profile
```

Add:

```bash
export APP_NAME="MyApp"
export JAVA_HOME="/usr/lib/jvm/java-17-openjdk"
export PATH=$JAVA_HOME/bin:$PATH
```

Apply the changes to the current shell:

```bash
source /etc/profile
```

> **Note:** `/etc/profile` affects login shells. It is usually better to avoid modifying this file directly when a dedicated file under `/etc/profile.d/` can be used.

---

## Method 3: `/etc/profile.d/` — Best Practice

Create a dedicated configuration file:

```bash
sudo nano /etc/profile.d/custom_env.sh
```

Add:

```bash
export APP_NAME="MyApp"
export JAVA_HOME="/usr/lib/jvm/java-17-openjdk"
export PATH=$JAVA_HOME/bin:$PATH
```

Apply the changes:

```bash
source /etc/profile.d/custom_env.sh
```

Or log out and log back in.

This approach is recommended because custom environment variables remain separate from the main system configuration files.

---

## User-Level vs System-Wide Variables

| Configuration         | Scope        | Typical Use                            |
| --------------------- | ------------ | -------------------------------------- |
| `~/.bashrc`           | Current user | User-specific variables                |
| `~/.zshrc`            | Current user | Zsh user configuration                 |
| `/etc/environment`    | All users    | Simple system-wide variables           |
| `/etc/profile`        | All users    | Login-shell configuration              |
| `/etc/profile.d/*.sh` | All users    | Custom system-wide shell configuration |

---

## Summary

| File                  | Scope                   | Supports `export` |                         Recommended |
| --------------------- | ----------------------- | ----------------: | ----------------------------------: |
| `/etc/environment`    | All users               |                No |            Yes for simple variables |
| `/etc/profile`        | All users, login shells |               Yes |                                Good |
| `/etc/profile.d/*.sh` | All users, login shells |               Yes |                    ⭐ Best Practice |
| `~/.bashrc`           | Current user            |               Yes | ⭐ Best for user-specific variables |

---

## Quick Reference

```bash
# View all variables
printenv

# View one variable
echo $HOME

# Create temporary variable
export APP_NAME="MyApp"

# Remove variable
unset APP_NAME

# Add permanent user variable
nano ~/.bashrc

# Reload user configuration
source ~/.bashrc

# System-wide variables
sudo nano /etc/environment

# System-wide shell configuration
sudo nano /etc/profile.d/custom_env.sh

# Reload custom system-wide configuration
source /etc/profile.d/custom_env.sh
```
