# Redo

An implementation of djb's [redo](http://cr.yp.to/redo.html) that I made a while ago.
My goal was to learn a bit about Perl.

Redo is a build system that allows for recursive and atomic rebuilds.

This endeavour was in ispired by jekor's video series
[Haskell from Scratch](https://www.youtube.com/playlist?list=PLxj9UAX4Em-Ij4TKwKvo-SLp-Zbv-hB4B).

## Installation

Install the executable and a symlink to a directory in your `$PATH`, e.g.:

```bash
install redo $HOME/.local/bin
ln -s $HOME/.local/bin/redo $HOME/.local/bin/redo-ifchange
```

## Usage

An example project can be found in the `example` directory.

```bash
cd example
redo hello_world
```

## Known Bugs

Builds in parent directories (e.g. `redo ../some/target`) don't work because this will generate the
digest files in `$PWD` rather than `$PWD/.redo/`.
Maybe, this can be fixed by, when executing `redo some/path/target`, switching the working directory 
to `some/path/`, then building, then switching back to write the digest files to `.redo/`.
I'm not sure though, where to put the digests; maybe I could just strip any leading `../` parts.
This will still not work for cases where a .do script contains `redo-ifchange ../some/target`.

## Possible enhancements

A program `redo-clean [<target>]` as a counterpart to `make clean`.
This would have to gather the names of all targets from `.redo/`, remove these targets, and finally
remove `.redo`.
