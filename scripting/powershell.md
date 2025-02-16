# PowerShell Scripting CheatSheet

A comprehensive guide covering essential PowerShell scripting commands for automation, system administration, and task automation.

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
- [PowerShell Remoting](#powershell-remoting)
- [Error Handling](#error-handling)
- [Logging](#logging)
- [PowerShell Modules](#powershell-modules)

## Getting Started

Run a PowerShell script:
```powershell
./script.ps1
```

Run PowerShell as Administrator:
```powershell
Start-Process powershell -Verb runAs
```

## Variables & Data Types

Define a variable:
```powershell
$variable = "Hello, PowerShell"
```

Check variable type:
```powershell
$variable.GetType()
```

## Operators

Arithmetic operators:
```powershell
$sum = 5 + 3
```

Comparison operators:
```powershell
5 -eq 5   # Equals
5 -ne 3   # Not Equals
5 -gt 3   # Greater Than
```

Logical operators:
```powershell
($a -eq $b) -and ($c -ne $d)
```

## Conditional Statements

```powershell
if ($x -gt 10) {
    Write-Host "Greater than 10"
} elseif ($x -eq 10) {
    Write-Host "Equals 10"
} else {
    Write-Host "Less than 10"
}
```

## Loops

For loop:
```powershell
for ($i=0; $i -lt 5; $i++) {
    Write-Host $i
}
```

While loop:
```powershell
while ($x -lt 10) {
    $x++
}
```

Foreach loop:
```powershell
foreach ($item in $array) {
    Write-Host $item
}
```

## Functions

Define a function:
```powershell
function Greet {
    param ($name)
    Write-Host "Hello, $name!"
}
```

Call a function:
```powershell
Greet "Arpit"
```

## Working with Files & Directories

List files in a directory:
```powershell
Get-ChildItem "C:\path"
```

Create a new file:
```powershell
New-Item -ItemType File -Path "C:\path\file.txt"
```

Delete a file:
```powershell
Remove-Item "C:\path\file.txt"
```

## Working with Processes

List running processes:
```powershell
Get-Process
```

Kill a process:
```powershell
Stop-Process -Name "notepad"
```

## Networking

Check internet connectivity:
```powershell
Test-NetConnection google.com
```

Get local IP address:
```powershell
Get-NetIPAddress
```

## System Administration

Get system info:
```powershell
Get-ComputerInfo
```

Restart computer:
```powershell
Restart-Computer
```

## Working with Services

List all services:
```powershell
Get-Service
```

Start a service:
```powershell
Start-Service -Name "wuauserv"
```

Stop a service:
```powershell
Stop-Service -Name "wuauserv"
```

## PowerShell Remoting

Enable remoting:
```powershell
Enable-PSRemoting -Force
```

Run command on remote machine:
```powershell
Invoke-Command -ComputerName Server01 -ScriptBlock { Get-Process }
```

## Error Handling

Try-Catch block:
```powershell
try {
    Get-Item "C:\NonExistentFile.txt"
} catch {
    Write-Host "Error: $_"
}
```

## Logging

Write to a log file:
```powershell
"Log Entry" | Out-File -FilePath "C:\log.txt" -Append
```

## PowerShell Modules

List installed modules:
```powershell
Get-Module -ListAvailable
```

Install a module:
```powershell
Install-Module -Name Az -Force
```

Import a module:
```powershell
Import-Module -Name Az
```