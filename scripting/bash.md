# Bash Scripting CheatSheet

A comprehensive guide covering essential Bash scripting commands for automation, system administration, and DevOps tasks.

## Table of Contents

- [Getting Started](#getting-started)
- [Variables & Data Types](#variables--data-types)
- [Operators](#operators)
- [Conditional Statements](#conditional-statements)
- [Loops](#loops)
- [Functions](#functions)
- [Working with Files & Directories](#working-with-files--directories)
- [Working with Processes](#working-with-processes)
- [Networking](#networking)
- [System Administration](#system-administration)
- [Working with Services](#working-with-services)
- [Error Handling](#error-handling)
- [Logging](#logging)
- [Bash Modules](#bash-modules)

## Getting Started

Run a Bash script:
```bash
./script.sh
```

Make a script executable:
```bash
chmod +x script.sh
```

Run Bash interactively:
```bash
bash
```

## Variables & Data Types

Define a variable:
```bash
variable="Hello, Bash"
echo $variable
```

Read user input:
```bash
read -p "Enter name: " name
echo "Hello, $name"
```

## Operators

Arithmetic operators:
```bash
sum=$((5 + 3))
echo $sum
```

Comparison operators:
```bash
[ 5 -eq 5 ]   # Equals
[ 5 -ne 3 ]   # Not Equals
[ 5 -gt 3 ]   # Greater Than
```

Logical operators:
```bash
[ "$a" = "$b" ] && echo "Equal"
[ "$a" != "$b" ] || echo "Not Equal"
```

## Conditional Statements

```bash
if [ $x -gt 10 ]; then
    echo "Greater than 10"
elif [ $x -eq 10 ]; then
    echo "Equals 10"
else
    echo "Less than 10"
fi
```

## Loops

For loop:
```bash
for i in {1..5}; do
    echo $i
done
```

While loop:
```bash
while [ $x -lt 10 ]; do
    x=$((x+1))
done
```

Foreach loop:
```bash
for item in ${array[@]}; do
    echo $item
done
```

## Functions

Define a function:
```bash
function greet() {
    echo "Hello, $1!"
}
```

Call a function:
```bash
greet "Arpit"
```

## Working with Files & Directories

List files in a directory:
```bash
ls -l /path
```

Create a new file:
```bash
touch /path/file.txt
```

Delete a file:
```bash
rm /path/file.txt
```

## Working with Processes

List running processes:
```bash
ps aux
```

Kill a process:
```bash
kill -9 <PID>
```

## Networking

Check internet connectivity:
```bash
ping -c 4 google.com
```

Get local IP address:
```bash
hostname -I
```

## System Administration

Get system info:
```bash
uname -a
```

Restart computer:
```bash
sudo reboot
```

## Working with Services

List all services:
```bash
systemctl list-units --type=service
```

Start a service:
```bash
sudo systemctl start apache2
```

Stop a service:
```bash
sudo systemctl stop apache2
```

## Error Handling

Try-Catch equivalent in Bash:
```bash
if ! ls /nonexistentfile 2>/dev/null; then
    echo "Error: File not found"
fi
```

## Logging

Write to a log file:
```bash
echo "Log Entry" >> /var/log/script.log
```

## Bash Modules

List available modules:
```bash
compgen -A function
```

Import a module (source a script):
```bash
source script.sh
```