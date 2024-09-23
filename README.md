# `resize` - reset TERMCAP with current size of a telnet window

This program was extracted from the 1986
[X Version 10 Release 3 archive](https://www.x.org/releases/X10R3/)
for use on for vintage BSD 2.11 & BSD 4.3 systems. The only change was
to make the copyright file a local include (and to add this README).

## SYNOPSIS

resize

## DESCRIPTION

`resize` prints on its standard output the TERM and TERMCAP commands
for the C-shell of the current size of a window. It is never executed
directly by the user, but should be aliased similarly to
`tset` to cause the C-shell to execute the commands.

**Note:**
This command is *not* required for remote logins via `rlogin`/`rsh`
(or modern `slogin`/`ssh`), which automatically forward changes in
terminal window size.
This command is only required for the console, local ttys, and remote
`telnet` sessions.

### Example

The following alias when executed as a command will reset
the environment of the current shell:

```csh
alias xs  'set noglob; eval `resize`'
```

## FILES

* `/etc/termcap` for the base termcap entry to modify.
* `~/.cshrc` user's alias for the command.

## "SEE ALSO"

rlogin(1), csh(1), tset(1), xterm(1)

## AUTHORS

Mark Vandevoorde (MIT-Athena)

Copyright (c) 1984, 1985 by
[Massachusetts Institute of Technology](https://www.mit.edu).
See the [full text of the copyright](mit-copyright.h).

## BUGS

Ought to be able to generate the strings for the Bourne shell.

If at user login, the terminal window is not the default defined size
(usually 80x24) on a vintage system which does not check the actual
window size, `resize` should be run in `.login`.

Likewise, if after login the user changes the terminal window size on a
vintage system, `resize` must be run again. Aliases can run perform this
`resize` automatically prior to select full screen programs:

```csh
alias   less    'set noglob ; eval `resize` ; "less" '
alias   man     'set noglob ; eval `resize` ; "man" '
alias   more    'set noglob ; eval `resize` ; "more" '
alias   vi      'set noglob ; eval `resize` ; "vi" '
```

**Note**: If relying on `resize`, changing the window size once a command
is running won't be seen by the program. You must exit the program, run
`resize`, and restart the program.

The vintage `vi` editor may default to a small window size inappropriate
for fast network connected terminals.  It can be helpful to modify
`.exrc` to force a full screen window:

```vi
set window=99
```
(*Hey, the last of the hardcopy TTYs running at 10 CPS still shattered
the quiet of terminal rooms when `ex` and vi were written. Small windows were useful ... once.*)
