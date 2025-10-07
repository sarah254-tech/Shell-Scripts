# 🐚 Shell Scripting 

 **🔎 Why learn shell scripting?**

Shell scripts let you automate repetitive Linux tasks, glue tools together, and run lightweight services or monitors on any machine. They are essential for DevOps, administration, CI/CD, and quick prototyping.

## 🧭 Core Concepts (quick flow)

### 1. Shebang & execution

`#!/usr/bin/env bash`
`# or: #!/bin/bash`

Put the shebang as the first line to tell the system which shell to use.

Make the script executable: `chmod +x script.sh`

Run: `./script.sh` or `bash script.sh` (Assuming you have a file created by the name script.sh)

Before we dive into writing a script here are some of the basic syntaxes and how to apply them, the do's and Donts

# 🐚 Shell Scripting Syntax Cheat Sheet (Quick Reference)

A concise guide to the essential **Bash syntax**, with examples and best practices, ideal for beginners and DevOps learners.



## 📘 Basic Structure

| Syntax / Command | Description | Example |
|------------------|--------------|----------|
| `#!/usr/bin/env bash` | Shebang line — defines script interpreter | `#!/bin/bash` |
| `# comment` | Add script comments | `# This is a comment` |
| `chmod +x script.sh` | Make script executable | `chmod +x backup.sh` |
| `./script.sh` | Run a script | `./hello.sh` |



## 🔠 Variables & Strings

| Syntax | Description | Example |
|---------|--------------|----------|
| `var=value` | Define variable (no spaces) | `name="Sarah"` |
| `$var` | Access variable | `echo "Hello $name"` |
| `"${var}"` | Use quotes to prevent splitting | `echo "File: ${file}"` |
| `$(command)` | Command substitution | `today=$(date +%F)` |
| `` `command` `` | Legacy substitution (avoid) | `` now=`date` `` |



## 🔢 Arithmetic & Comparisons

| Syntax | Purpose | Example |
|---------|----------|----------|
| `$((expression))` | Perform arithmetic | `sum=$((a + b))` |
| `((a++))` | Increment variable | `((count++))` |
| `[[ $a -eq $b ]]` | Numeric comparison | `[[ $age -ge 18 ]]` |
| `[[ $a == $b ]]` | String comparison | `[[ $name == "Sarah" ]]` |
| `[[ -f file ]]` | File test (exists and is a file) | `[[ -f script.sh ]]` |
| `[[ -d dir ]]` | Directory test | `[[ -d /etc ]]` |



## 🔄 Conditionals

| Syntax | Description | Example |
|---------|--------------|----------|
| `if [[ condition ]]; then ... fi` | Basic if statement | `if [[ $age -gt 18 ]]; then echo "Adult"; fi` |
| `elif [[ condition ]]; then` | Else if condition | `elif [[ $age -eq 18 ]]; then echo "Just 18"` |
| `else` | Fallback branch | `else echo "Minor"` |
| `[ condition ]` | POSIX test form | `[ -e file.txt ]` |



## 🔁 Loops

| Syntax | Description | Example |
|---------|--------------|----------|
| `for i in {1..5}; do ... done` | For loop | `for i in {1..3}; do echo $i; done` |
| `for f in *.txt; do ... done` | Loop through files | `for f in *.log; do echo $f; done` |
| `while [[ condition ]]; do ... done` | While loop | `while [[ $count -lt 5 ]]; do ((count++)); done` |
| `until [[ condition ]]; do ... done` | Loop until true | `until [[ $n -gt 3 ]]; do ((n++)); done` |



## 🧠 Case Statement

| Syntax | Description | Example |
|---------|--------------|----------|
| `case $var in pattern)` | Multi-choice branching | `case $option in start) echo "Start";; stop) echo "Stop";; esac` |
| `*)` | Default pattern | `*) echo "Invalid";;` |



## 🧰 Functions

| Syntax | Description | Example |
|---------|--------------|----------|
| `function name() { ... }` | Define a function | `greet() { echo "Hi $1"; }` |
| `name args` | Call a function | `greet Sarah` |
| `$1, $2, $@` | Positional parameters | `echo "Arg1: $1"` |
| `return n` | Return status (0 = success) | `return 0` |
| `result=$(func)` | Capture output | `msg=$(say_hello)` |



## 📂 File & Directory Tests

| Flag | Description | Example |
|------|--------------|----------|
| `-e` | File exists | `[[ -e data.csv ]]` |
| `-f` | Regular file | `[[ -f report.txt ]]` |
| `-d` | Directory exists | `[[ -d /var/log ]]` |
| `-r` | Readable | `[[ -r notes.md ]]` |
| `-w` | Writable | `[[ -w /tmp/test ]]` |
| `-x` | Executable | `[[ -x script.sh ]]` |



## 🗣️ Input & Output

| Syntax | Description | Example |
|---------|--------------|----------|
| `read var` | Prompt for input | `read name` |
| `read -p "Prompt: " var` | Inline prompt | `read -p "Enter name: " user` |
| `>` | Redirect output (overwrite) | `echo "Hello" > log.txt` |
| `>>` | Append output | `echo "New" >> log.txt` |
| `2>` | Redirect errors | `ls /bad/path 2> errors.log` |
| `&>` | Redirect all output | `command &> output.log` |



## 📜 Arrays

| Syntax | Description | Example |
|---------|--------------|----------|
| `arr=(a b c)` | Declare array | `fruits=("apple" "banana" "mango")` |
| `${arr[0]}` | Access element | `echo ${fruits[0]}` |
| `${arr[@]}` | All elements | `for i in "${fruits[@]}"; do echo $i; done` |
| `${#arr[@]}` | Length | `echo ${#fruits[@]}` |



## 🧾 Exit Codes

| Syntax | Description | Example |
|---------|--------------|----------|
| `$?` | Status of last command | `ls; echo $?` |
| `exit n` | Exit with code `n` | `exit 1` |
| `set -e` | Exit on error | Add to top of script |
| `set -u` | Error on unset variable | Add to top of script |



## 🔄 Command Control

| Command | Description | Example |
|----------|--------------|----------|
| `cmd1 && cmd2` | Run 2 if 1 succeeds | `mkdir test && cd test` |
| `cmd1 || cmd2` | Run 2 if 1 fails | `ping -c1 google.com || echo "No network"` |
| `cmd &` | Run in background | `./script.sh &` |
| `jobs` | List background jobs | `jobs -l` |
| `fg %1` | Bring job to foreground | `fg %1` |
| `kill PID` | Stop process | `kill 2345` |



## 🧱 Traps & Cleanup

| Syntax | Description | Example |
|---------|--------------|----------|
| `trap 'cmd' EXIT` | Run command on exit | `trap 'rm -f /tmp/tempfile' EXIT` |
| `trap 'cmd' INT` | Catch Ctrl+C | `trap 'echo Interrupted' INT` |



## 🧩 Debugging

| Command | Description | Example |
|----------|--------------|----------|
| `bash -x script.sh` | Trace execution | `bash -x run.sh` |
| `set -x` | Enable debug in script | `set -x` |
| `set +x` | Disable debug | `set +x` |
| `set -euo pipefail` | Strict mode (exit on errors) | Place at script top |



## ✅ Do’s and 🚫 Don’ts Summary

| ✅ Do’s | 🚫 Don’ts |
|---------|------------|
| Use `#!/usr/bin/env bash` for portability | Don’t mix `sh` and `bash` syntax |
| Quote all variables `"${var}"` | Don’t leave `$var` unquoted (causes splitting) |
| Use `set -euo pipefail` for safety | Don’t ignore failed commands |
| Test with `bash -x` before deploying | Don’t run destructive commands blindly |
| Use lowercase for local vars | Don’t override system vars like `$PATH` |
| Log actions and results | Don’t suppress errors (`2>/dev/null`) unless necessary |
| Comment logically and consistently | Don’t fill scripts with redundant info |



## 🧠 Pro Template for All Scripts


`#!/usr/bin/env bash`
`set -euo pipefail`
`IFS=$'\n\t'`

`#Author: <Your Name>`
`#Description: <Short explanation>`
`#Usage: ./script.sh [options]`

`main()`
`{`
`echo "Script starting..."`
`# your logic here`
`}`

**✅ Safe — prevents silent errors**
**✅ Portable — works across distros**
**✅ Professional — clean entry point and structure**

## Rule

### 🧩 “Write shell scripts like blueprints, simple, modular, and reusable.” 



