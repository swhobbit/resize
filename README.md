# `resize` - reset TERMCAP with current size of a window

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
`tset`

to cause the C-shell to execute the commands.

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

csh(1), tset(1), xterm(1)

## AUTHORS

Mark Vandevoorde (MIT-Athena)

Copyright (c) 1984, 1985 by
[Massachusetts Institute of Technology](https://www.mit.edu).
See the [full text of the copyright](mit-copyright.h).

## BUGS

Ought to be able to generate the strings for the Bourne shell.

If at user login, the terminal window is not the default defined size
(usually 80x24) on a vintage system which does not the propagate window
change signal (`SIGWINCH`), resize should be run in `.login`.

Likewise, if after login the user resizes the terminal window on a vintage
system, resize must be run again. Aliases can run perform this resize
automatically prior to select full screen programs:

```csh
alias   more    'eval `resize` ; "more" '
alias   less    'eval `resize` ; "less" '
alias   vi      'eval `resize` ; "vi" '
```

The vintage `vi` editor often defaults to a small window size
inappropriate for fast network connected terminals.  It can be helpful
to modify `.exrc` to force a full screen window:

```vi
set window=99
```

Modern UNIX/BSD/Linux systems generally propagate the window
change signal; full screen programs (like editors, pagers and
games) then handle it properly. Using resize is never required
on such systems.
