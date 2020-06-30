# 9front-screenshots
An easy way to transfer screenshots from Plan9 to other places
Especially serves as a visual demo for successfully (re-)ported
programs which are under their own repos.

Below is an overview of my Plan9 ([[9front]](http://9front.org/)) porting projects.
For most of the ports I am generating mk files so appart from having
potential dependencies available, it should be as simple as "mk install".
The vast majority of the ports aim to lower the threshold for building alien
software under APE by providing common dependencies.

My hope is that many of these ports will be obsoleted by nicer and more native
solutions within APE in the future. 

This is in a way a revival of my old [["ports2plan9"]](https://code.google.com/archive/p/ports2plan9) project,
which included [[GNU on Plan9]](https://code.google.com/archive/p/ports2plan9/wikis/GNUonPlan9.wiki).

But as they say "The best is the enemy of the good". Here I provide "good enough"
solutions for now.

# This serves as an overview of various ports I am making to Plan9 (9front)

## GCC tool chain
There are old i386-plan9 ports available, like

[[gcc 3.0 and binutils 2.11]](https://9p.io/sources/extra/gcc/) : [[diff (gcc)]](https://github.com/staalmannen/gcc/pull/2) and [[diff (binutils)]](https://github.com/staalmannen/binutils-gdb/pull/1/files)

and

[[gcc 4.8.3 and binutils 2.22]](https://marcus.biz.tm/jail/) : [[diff (gcc)]](https://github.com/staalmannen/gcc/pull/3) and [[diff (binutils)]](https://github.com/staalmannen/binutils-gdb/pull/3/files)


The aim here is to keep those changes integrated in a VCS so that it will be easier
to update those changes to the latest version.

Binutils : https://github.com/staalmannen/binutils-gdb
GCC : https://github.com/staalmannen/gcc
LibC : https://github.com/staalmannen/gcc-apelibs

TODO : need to get them to work. It would be great to also package them as cross-
compilers. Also getting more architecture support than i386 woudld be great.


## GNU utilities
Many programs expect GNU-specific behavior during configuration / building.
These are some common dependencies that I try to solve. Some of these 
could also make sure that the GCC tool chain (above) is as small as possible
and that most of the required tools are built with the native tool chain.

### gawk
https://github.com/staalmannen/gawk

Why?: Yet again, sometimes required during configuration.

status: Does not build.

The old port can be found here:
https://9p.io/sources/contrib/staal1978/pkg/gawk-4.0.0b.pkg.tbz

### gmake
https://github.com/staalmannen/make

why? : APE make usually good but sometimes gmake is needed during cofigure.

status: Builds but seem to not work. Older versions worked. I had some development
logistics issues and made lots of tiny commits to try to fix a bitfield issue in
2 files. There may be some kind of bug that crept in there.

The old port can be found here:
https://9p.io/sources/contrib/staal1978/pkg/gmake-3.82b.tbz

### gsed
https://github.com/staalmannen/sed

why? : Some configure scripts need it and "gsed -i" is just too convenient.

status: Does not build. 

The old port can be found here:
https://9p.io/sources/contrib/staal1978/pkg/gsed-4.2.1c.tbz


## GNU libraries
It is also very common that certain posix features are missing in APE,
and GNU offers some portable solutions. Many of them are old and not
in active development. 

### libutf8
https://github.com/staalmannen/libutf8

Why?: wchar* stuff a very common dependency.

status: It builds and I have built PDCurses with it as an optional variant and it worked just fine.
More testing (like always) is probably needed.

### Pth
https://github.com/staalmannen/phtsem

Why?: Pthread is a very common dependency.

status: The library builds. Still needs more testing


## Common libraries

### PCRE
https://github.com/staalmannen/pcre

Status: it builds and the included programs build.

### PDCurses
https://github.com/staalmannen/PDCurses

Status: It builds, demos and programs built with it works.
There are pull request to get the Plan9 support to upstream and 
to a very active fork with many extra experimental features.

## Other apps

### BSDgames
https://github.com/staalmannen/BSDGames

why?: A bunch of small games are always fun. Also a demo of the capabilities of the
PDCurses port.

Status: I am currently building/porting it...

### nbsdgames
https://github.com/staalmannen/nbsdgames

Why: Mostly as a test/demonstration of PDCurses on Plan9. 
Issues encountered: I had to hack a bit because the Plan9 compiler can not handle VLAs.

This one has already been integrated upstream:
https://github.com/abakh/nbsdgames


### NetHack
https://github.com/staalmannen/NetHack

Why: Would be very cool to have it.

Status: Stuck at bitfields issues during compilation.

### Zsh
https://github.com/staalmannen/zsh

Why?: I have built/ported [[mksh]](http://mail.9fans.net/pipermail/9fans/2013-July/028031.html) before but it could only be on i386 and had limited
functionality. An alternative APE posix shell is needed sometimes for some scripts that
are not working on the old ksh port that is ape/sh.

Status: Surprisingly, it builds! (depends: pdcurses, pcre. terminfo(pdterm)).
But it does not work... Some debugging needed thus...







