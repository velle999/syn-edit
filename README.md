# syn-edit

A text editor that is modal in a terminal and modeless in a window, with
syntax highlighting in both. The same engine is underneath, so a file edited
one way behaves the same the other way.

## Editing

```bash
syn-edit file.c              # the terminal editor: i to insert, :w, :q
syn-edit gui file.c          # the window
syn-edit langs               # every language that is highlighted
```

The terminal editor is vi-shaped — motions, operators, counts, registers,
`:` commands. The window is not: it types where you click, `Ctrl+S` saves,
and the modal keys are available through `gui insert` and friends for anyone
who wants them.

## Scripting the same engine

The editor's engine runs without a terminal, which makes it useful in a
pipeline and is how it is tested:

```bash
syn-edit run file.txt -k 'ggdG'          # apply keys, print the result
syn-edit run file.txt -c '%s/a/b/g' -w   # an ex command, written back
syn-edit ex file.txt -c '1,5d'           # only ex commands
syn-edit highlight file.c                # the syntax spans it scans to
```

`--status` prints the cursor, mode and message as records, so a front end can
drive the engine and draw its own screen.

## Notes

The graphical window needs `quickshell`. `wl-clipboard` gives it the desktop
clipboard, reached as the `+` register (`"+y`, `"+p`). `syn-edit about` says
which of these are present on the machine it is run on.

## Install

```bash
git clone https://github.com/velle999/syn-edit
cd syn-edit && makepkg -si
```

makepkg fetches the source for this PKGBUILD's exact version from this
repository's releases, so a clone can only ever build the source it was
written against. `.SRCINFO` lists what it needs.

## Where this comes from

Developed in [the SynapseOS monorepo](https://github.com/velle999/SYNAPSE),
in `syn-edit/`. **This repository is generated from it** — the PKGBUILD, a
generated `.SRCINFO` and this README — so issues and patches belong there.

syn-edit 0.1.0-20 · GPL-2.0-or-later
