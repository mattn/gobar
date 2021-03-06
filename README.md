[![Build Status](https://travis-ci.org/KenjiTakahashi/gobar.png?branch=master)](https://travis-ci.org/KenjiTakahashi/gobar)

**gobar** is a minimalistic X status bar written in pure Go.

Supports xinerama, EWMH, font antialiasing and possibly some other fancy looking names and shortcuts.

## screenshot

Two **gobar** instances.

Top with some conky metrics.
Bottom with wingo workspaces (bash + wingo-cmd for now) and date.

![screenshot](https://copy.com/eIedmSWFgREV)

## installation

First, you have to [get Go](http://golang.org/doc/install). Note that version >= 1.1 is required.

Then, just

```bash
$ go get github.com/KenjiTakahashi/gobar
```

should get you going.

## usage

Command line options reference follows:

**-h --help** displays help message and exits.

**--bottom** places bar on bottom of the screen (default is on top).

**--geometry=** takes comma separated list of monitor geometries.

Each geometry element is in form of `<width>x<height>+<x>+<y>`. Where `<width>` can also take a special value of `M`, meaning "take all available space".

If omitted, or if number of specified geometries is lower than number of monitors, a default of `Mx16+0+0` is used for not specified monitors.

**--fonts=** takes comma separated list of fonts.

Each font element is in form of `<ttf file path>:<font size>`.

Defaults to `/usr/share/fonts/TTF/LiberationMono-Regular.ttf:12`. Which is probably no good and will be changed.

**--fg=** takes main foreground color. Should be in form `0xAARRGGBB`.

**--bg=** takes main background color. Should be in form `0xAARRGGBB`.

Other than that, an input string should be piped into the **gobar** executable.

A really simple example could be displaying current date and time.
```bash
$ while :; do date; sleep 1; done | gobar
```

Special tokens can also be used in the input string to allow nice formatting.

#### Input string formatting syntax

Each token should be preceded with `{` and will be active until `}`.

**F&lt;num&gt;** sets active font, **&lt;num&gt;** should be index of one of the elements from fonts list specified in **--fonts=**.

**S&lt;num&gt;,&lt;num&gt;...** specifies monitors to draw on. Multiple, comma separated, numbers can be specified. If not specified, draws to all available monitors.

**CF0xAARRGGBB** sets active foreground color.

**CB0xAARRGGBB** sets active background color.

**AR** aligns next text piece to the right.
