# starter

POSIX shell script and function to schedule commands

(C) Martin Väth (martin at mvath.de).
This project is under the BSD license.

## Warning

This project is practically no longer maintained.
Unless you have a special reason, use instead the successor project
https://github.com/vaeth/schedule

## Description

This script can be used to schedule commands in a multitasking
and multiuser environment.

Commands started with this script will wait with the execution
until all commands started earlier with this script
(possibly by a different user) have been executed.

You can also have several of such command queues or add a command
to a queue even if you start it immediately.

## Usage
To get help about the usage, call

`starter -h`

There is also a `starter_trap` function available for execution of
commands within your current shell. To obtain this function use either

```eval `starter_trap` ```

or

`. starter_trap`

in your current shell or put the following into your shell startup files:
```
starter_trap() {
	if starter_trap=`starter_trap 2>/dev/null`
	then	eval "$starter_trap"
	else	echo "starter_trap not found" >&2
		return 1
	fi
	starter_trap ${1+"$@"}
}
```
Information about the `starter_trap` function can then be obtained with

`starter_trap -h`

## Installation

For installation, copy the content of `bin/` in your `$PATH`.
You also need `push.sh` from https://github.com/vaeth/push in your `$PATH`.
If you want that the hard status line is set, also the `title` script from
https://github.com/vaeth/runtitle (version 2.3 or newer) is required in your
`$PATH`.
To obtain support for __zsh completion__, you can copy the content of `zsh/`
to a directory of your zsh's `$fpath`.

For Gentoo, there is an ebuild in the mv overlay (available over layman).
