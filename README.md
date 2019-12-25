# Run

A universal utility for running programs

## Usage

```text
run filename.ext
```

Run the program `filename.ext` using the rule `ext`, which is specified in `rules/ext`.

```text
run -r ext2 filename.ext
run --rule ext2 filename.ext
```

Run the program `filename.ext` using the rule `ext2`.

```text
run -c
run --clean
```

Delete any compiled object generated by `run`.

```text
run -c dir
run --clean dir
```

Delete any compiled object generated by `run` in the directory `dir`.


```text
run -h
run --help
```

Display help.


## Rule Specification

All rules are specified in files located in the `rules` directory. Each rule is a series of commands, one per line. The type of command is determined by the first character in the line.

| First character | Significance |
|-----|------------------------|
| `!` | The rest of that line is executed as a bash command. If any command fails, `run` stops and exits with the same exit status. |
| `>` | It will mark the file following it as a compiled object. Following on the same line is the list of prerestiquites for that object. The following block of lines specify how to compile that object. Compilation only occurs if objects are not up to date. |
| `$` | The line ends a block. |
| `#` | The line is a comment. |

The character `@` is replaced with `filename` (absolute path not including `.ext`) wherever it is found in the rule file.
