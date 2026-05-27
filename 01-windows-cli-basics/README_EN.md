# Windows PowerShell Basics Lab

## Overview

This lab demonstrates fundamental concepts of file and directory management using PowerShell in Windows.

The environment focuses on using the Command Line Interface (CLI) to perform basic tasks such as navigation, creation, copying, moving, renaming, and deleting files and folders.

It also covers relative and absolute paths, wildcards, and advanced PowerShell parameters commonly used in system administration and technical support tasks.

---

## Objectives

- Navigate between directories using PowerShell  
- Understand relative and absolute paths  
- Create files and folders from the CLI  
- Copy files using wildcards  
- Move and rename files  
- Delete files and directories  
- Use advanced parameters such as `-Recurse` and `-Force`  
- Validate results using verification commands 

---

## Technologies Used

- Windows 11  
- PowerShell  
- CLI (Command Line Interface)  
- Windows file system  

## Lab Structure

```text
Desktop
 ├── test_folder
 │    ├── file1.txt
 │    ├── file2.txt
 │    └── image1.jpg
 │
 ├── backup
 │
 └── Pics
```
## Navigation Between Directories

Navigation between folders was practiced using relative and absolute paths.

### Commands Used

```bash
pwd
ls
cd
cd ..
cd ~
cd ~\Desktop
```

## Applied Concepts

- Directory navigation
- Relative and absolute paths
- User home directory (~)
- Parent directory (..)

## File and Folder Creation

### Commands Used

```bash
mkdir test_folder
mkdir backup
mkdir Pics

New-Item file1.txt
New-Item file2.txt
New-Item image1.jpg
```
## File and Directory Copying

### Commands Used
```bash
cp *.txt ../backup
cp *.jpg ../Pics
cp test_folder backup -Recurse
```
## Verification
```
ls ../backup
ls ../Pics
```
## Moving and Renaming

### Commands Used

```bash
mv file1.txt document.txt
mv document.txt ../backup
```
## File and Directory Deletion

### Commands Used
```
rm file2.txt
rm test_folder -Recurse
rm image1.jpg -Force
```
## History and Productivity
```
history
clear
```
## Functions Used

- Command history
- Navigation using arrow keys ↑ ↓
- TAB autocompletion
- Screen clearing

## Key Concepts Learned

- CLI navigation
- Basic file and directory management
- Relative and absolute paths
- PowerShell wildcards
- File moving and renaming
- Recursive directory deletion
- Verification using CLI commands

## Skills Demonstrated

- PowerShell usage
- Basic Windows system administration
- File and directory management
- Basic CLI troubleshooting
- File structure organization
- Technical documentation

## Project Files
```
powershell-basics-lab/
│
├── README.md
├── README_EN.md
├── README_ES.md
│
├── docs/
│   ├── powershell-basics-lab_EN.pdf
│   └── powershell-basics-lab_ES.pdf
│
├── screenshots/
│   ├── figure1.png
│   ├── figure2.png
│   ├── figure3.png
│   └── figure4.png
```
## Notes

PowerShell provides an efficient way to manage Windows systems through CLI commands.
