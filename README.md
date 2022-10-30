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

- Allow deleting the files matched (with option to provide logs).

- Allow archiving a compressed copy of the files matched.

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
  -archive string
        Path to directory where files should be archived
  -del              
        Delete files
  -ext string
        File extension to filter out
  -list
        List files only
  -log string
        Log deletes to this file
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

#### Delete all files with `.log` extension inside `/tmp/testdir/` and its subdirectories:

```
$ walk -root /tmp/testdir/ -ext .log -del
```

#### Delete all files with `.txt` extension inside `/tmp/testdir/` and its subdirectories, and log deleted files to `deleted_files.log`:

```
$ walk -root /tmp/testdir -ext .txt -log deleted_files.log -del

$ cat deleted_files.log
DELETED FILE: 2022/10/15 21:02:15 /tmp/testdir/file1.txt
DELETED FILE: 2022/10/15 21:02:15 /tmp/testdir/text/text1.txt
DELETED FILE: 2022/10/15 21:02:15 /tmp/testdir/text/text2.txt
DELETED FILE: 2022/10/15 21:02:15 /tmp/testdir/text/text3.txt
```

#### Compress and archive all files with `.txt` extension inside `/tmp/testdir/` and its subdirectories, delete them after archiving, and log deleted files to `deleted_files.log`:

```
$ mkdir /tmp/testdir_txt_bkp

$ walk -root /tmp/testdir -ext .txt -archive /tmp/testdir_txt_bkp/ -log deleted_files.log -del

$ tree /tmp/testdir_txt_bkp
/tmp/testdir_txt_bkp
├── file1.txt.gz
└── text
    ├── text1.txt.gz
    ├── text2.txt.gz
    └── text3.txt.gz

$ cat deleted_files.log
DELETED FILE: 2022/10/30 19:18:30 /tmp/testdir/file1.txt
DELETED FILE: 2022/10/30 19:18:30 /tmp/testdir/text/text1.txt
DELETED FILE: 2022/10/30 19:18:30 /tmp/testdir/text/text2.txt
DELETED FILE: 2022/10/30 19:18:30 /tmp/testdir/text/text3.txt
```

## Backlog

- Add example Gif to README file.

- Allow the user to provide more than one file extension.

- Add more filtering options such as files modified after a certain date or files with long file names.

- Create a companion tool for walk that restores the archived files in case they are needed again. Recreate the original directory by using the same approach you used to create the destination directory in the `archiveFile` function. Then use the `gzip.Reader` type from the `compress/gzip` package to uncompress the archive files.

## Credits

_This is an exercise from the book "Powerful Command-Line Applications in Go", but it may differ from the original exercise._
