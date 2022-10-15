<h1 align="center">walk</h1>

*<p align="center">A CLI tool that walks a directory tree executing actions on files.</p>*

## About

Use the `walk` CLI tool to walk a directory tree listing or executing actions on files.

### Status:

[![Actions Status](https://github.com/rossijonas/walk/workflows/Test/badge.svg)](https://github.com/rossijonas/walk/actions)
[![Actions Status](https://github.com/rossijonas/walk/workflows/Build/badge.svg)](https://github.com/rossijonas/walk/actions)

### Features:

- Cross-platform:  Linux / macOS / Windows.

- Allow passing a directory path to walk in.

- Allow filtering by using a file extension. 

- Allow filtering by minimum file size.

- Allow executing actions on each file found. (⚠️ To do)

_(This is an exercise from the book "Powerful Command-Line Applications in Go".)_

## Installation

### Requirements:

- [Go](https://go.dev/) version 1.18.6 (or above)

### How to install:

- Run: 

  ```
  $ go install github.com/rossijonas/walk@latest
  ```

## Usage

### Options:

```
$ walk -h
Usage of walk:
  -ext string
        File extension to filter out
  -list
        List files only
  -root string
        Root directory to start (default ".")
  -size int
        Minimum file size
```

### Examples:

#### List all files inside the current directory and its subdirectories:

```
$ walk 
README.md
docs/mydocument.txt
photos/dog.jpg
```

#### List all files inside `/tmp/testdir/` and its subdirectories:

```
$ walk -root /tmp/testdir/
/tmp/testdir/file1.txt
/tmp/testdir/logs/log1.log
/tmp/testdir/logs/log2.log
/tmp/testdir/text/text1.txt
/tmp/testdir/text/text2.txt
```

#### List all files with `.log` extension inside `/tmp/testdir/` and its subdirectories:

```
$ walk -root /tmp/testdir/ -ext .log
/tmp/testdir/logs/log1.log
/tmp/testdir/logs/log2.log
```

## Backlog

- Add example Gif to README file.

- Allow executing actions in each file found.