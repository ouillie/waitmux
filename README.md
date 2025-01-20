# Waitmux

This tiny, standalone Bash script does one simple thing:
wait for the most recently started shell process to finish running.

## Why?

Bash makes it easy to run commands sequentially:
chain them together with `;`, or even `&&` if you want to be fault-aware.
But, this chaining only works if you remember to use it
*before* firing off that first command.

Let's say you want to shut down your machine
after the full system upgrade you just hit enter on,
but you forgot to add that `shutdown` command at the end.
You could either stare listfully screenward until your computer is safe to put down,
or you could switch to another terminal
and use this one simple trick to make sure `shutdown` runs after the update finishes:

```bash
waitmux && shutdown now
```

Waitmux finds that upgrade process and waits for it to finish before exiting,
giving you another chance to use a Bash `&&` chain.

## How?

Since figuring out which command to wait for could be error-prone,
this script assumes that the user always uses exactly one [tmux] session
to run all their shells.
This provides a narrower set of candidate processes to wait for,
ensuring that only an explicitly-typed command is selected.

[tmux]: https://github.com/tmux/tmux/wiki

If you don't use tmux, but like this general idea,
I'm sure it could be adapted to other use-cases.
