# minishell-c-shell42

A custom Unix-like shell written in C (42 minishell project style).  
It includes lexical analysis, parsing to an AST, expansion, redirections, and command execution with built-ins and external programs.

## Features

- Interactive prompt (`USER@PWD: ` when running in a TTY)
- Built-in commands:
  - `cd`
  - `echo` (supports `-n`)
  - `env`
  - `exit`
  - `export` (including `VAR+=value`)
  - `unset`
  - `pwd`
- External command execution through `PATH` resolution and `execve`
- Operators and control flow:
  - pipe: `|`
  - logical AND / OR: `&&`, `||`
  - subshells: `( ... )`
- Redirections:
  - input: `<`
  - output: `>`
  - append: `>>`
  - heredoc: `<<`
- Expansions:
  - environment variables (`$VAR`)
  - last command status (`$?`)
  - wildcard pathname expansion (`*`)
- Signal handling for interactive shell behavior (`Ctrl-C`, `Ctrl-\`, heredoc mode)

## Project layout

- `/src/lexer` — tokenization
- `/src/parsing` — AST construction and syntax handling
- `/src/expansion` — variable, field split, and wildcard expansion
- `/src/execution` — command execution, pipes, redirections, built-ins
- `/src/environment` — environment model, `PATH`, defaults (`PWD`, `SHLVL`, `_`)
- `/src/signals` — shell and heredoc signal handling
- `/src/shell` — prompt and shell loop
- `/libft` and `/ft_printf` — local dependencies used by the shell

## Requirements

- C compiler (`cc`)
- GNU Make
- Readline development headers/libraries
  - Debian/Ubuntu: `sudo apt install libreadline-dev`

## Build

From the repository root:

```bash
make
```

This builds:

- `libft/libft.a`
- `ft_printf/libftprintf.a`
- `libzen.a`
- executable: `./minishell`

## Run

```bash
./minishell
```

You can also pipe commands in non-interactive mode:

```bash
echo 'echo hello | cat' | ./minishell
```

## Available make targets

- `make` / `make all` — build project
- `make clean` — remove object files and `libzen.a`
- `make fclean` — `clean` + remove `minishell` and static libs
- `make re` — full rebuild

## Notes

- The project keeps command history through Readline history APIs.
- If parsing fails (for example, unclosed quotes or syntax errors), the shell reports errors and continues running.
