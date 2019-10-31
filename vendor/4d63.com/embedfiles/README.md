# embedfiles
[![Go Report Card](https://goreportcard.com/badge/github.com/leighmcculloch/embedfiles)](https://goreportcard.com/report/github.com/leighmcculloch/embedfiles)

Embedfiles is a tool for embedding files into Go code.

Files are stored in a map of filenames to file data.

## Install

### Source

```
go get 4d63.com/embedfiles
```

## Usage

```
$ embedfiles
Embedfiles embeds files into a map in a go file.

Usage:

  embedfiles -out=files.go -pkg=main <paths>

Flags:

  -file-names-var string
        name of the generated file names slice (default "fileNames")
  -files-var string
        name of the generated files slice (default "files")
  -out file
        output go file (default "files.go")
  -pkg package
        package name of the go file (default "main")
  -verbose
```

## Example

Given files:
```
$ echo "hello world" > file1
$ mkdir morefiles
$ echo "who are you?" > morefiles/file2
```

Embed with `embedfiles`:
```
$ embedfiles file1 morefiles
```

A new file `files.go` is created:
```
$ cat files.go
// Generated by 4d63.com/embedfiles.

package main

var fileNames = []string{
        "file1", "morefiles/file2",
}

var files = map[string][]byte{

        "file1": []byte{
                31, 139, 8, 0, 0, 0, 0, 0, 2, 255, 202, 72, 205, 201, 201, 87, 40, 207, 47, 202, 73, 225, 2, 4, 0, 0, 255, 255, 45, 59, 8, 175, 12, 0, 0, 0,
        },

        "morefiles/file2": []byte{
                31, 139, 8, 0, 0, 0, 0, 0, 2, 255, 42, 207, 200, 87, 72, 44, 74, 85, 168, 204, 47, 181, 231, 2, 4, 0, 0, 255, 255, 138, 46, 37, 108, 13, 0, 0, 0,
        },
}
```