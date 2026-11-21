# minishell

`minishell` is a small interactive Unix shell written in C. It reads commands
through GNU Readline, parses them into commands and files, expands variables,
and executes built-ins or external programs found through `PATH`. The
implementation is specific to this project and does not claim full Bash or
POSIX compatibility.

## Implemented features

The source code implements these behaviors:

- Built-ins: `echo`, `cd`, `pwd`, `export`, `unset`, `env`, and `exit`.
- Pipelines with multiple commands, such as `cmd1 | cmd2 | cmd3`.
- Redirections: input (`<`), output/truncate (`>`), append (`>>`), and
  here-documents (`<<`).
- Environment handling, including `export`, `unset`, `PATH` command lookup,
  `$NAME` expansion, and the previous status variable `$?`.
- Single and double quotes. Quotes are removed during argument construction;
  single-quoted text is not expanded, while expansion is processed inside
  double quotes.
- Interactive signal handling for `Ctrl-C` and `Ctrl-\`, including
  here-document input.
- Exit-status propagation for built-ins and child processes, including
  signal-related statuses (`130` for `SIGINT` and `131` for `SIGQUIT`).
  `exit` accepts a numeric argument, reports invalid numbers, and reports
  extra arguments.

These points are verified by reading the implementation. No automated test
suite or test target is defined in the Makefile.

## Requirements and usage

The Makefile uses `cc` and GNU Readline/History. It expects Readline to be
installed under `$HOME/.brew/opt/readline`, with headers in `include` and
libraries in `lib`; this is the layout used by the repository's build flags.

```sh
make
./minishell
```

