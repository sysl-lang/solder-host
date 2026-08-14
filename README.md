# solder-host

**[SOLDER](https://github.com/sysl-lang/solder) at a terminal** — the console the language is meant to
be met through, on a machine where it can be tried without a board in the way.

```
$ solder-host
SOLDER. Type a line, or BYE to leave.
solder> 5 3 + PR
8
solder> DEF SQUARE DUP * END
solder> 7 SQUARE PR
49
solder> 5 0 DO I PR SPACE LOOP
0 1 2 3 4
solder> [] 1 , 2 , 3 , PR
[1 2 3]
solder> BYE
```

## What is here

**Thirty lines, and none of them are about SOLDER.** The read-run-print loop is
`sh.sysl.solder.session`, in the language's own package, because there is going to be more than one
console — this, and a board over a serial cable — and a loop written out per platform is copies that
drift. What is left here is the only platform-dependent part: which streams the lines come from.

At a terminal that is `sysl.term.edit`'s editor over `sysl.posix.tty`'s raw mode, so a keystroke is
seen as it is typed and the line can be edited. With input redirected from a file or a pipe there is
no terminal to put out of the way, and then the editor is the wrong facility entirely: nothing is
being typed, nothing should be echoed, and `console_lines` reads a stream of lines instead. So
`solder-host < script.solder` works, and works better than it would through an editor.

## Building it

```
sysl build .
```

The language is an ordinary coordinate, so this builds from a fresh clone with nothing beside it.

## Licence

ISC — see `LICENSE`.
