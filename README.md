# Cgull browser
This is a fork of the [lariza browser](https://uninformativ.de/git/lariza),
a simple webkit GTK3 browser.

## Regular features
- A WebKit2 viewport
- An input box to change the URI or to search the current page
- Built-in download manager
- Indicator for web feeds
- Global content zoom
- Keybindings for zooming in, out and resetting zoom
- Cooperative instances using FIFOs
- Certificate trust store
- Bundled user-supplied JavaScripts (optional):
    - Link hints
- Bundled web extensions (optional):
- Adblock
- Keybindings toggle javascript
- Keybinding to manage history and bookmarks with external program
- Open the curent link with an external program
- A cgull.desktop file is automatically installed on `make install`
- Dedicated keys to get to a certain tab on (ctrl+`n`) where `n` is a number key
- Search CGULL_SEARCH_URI if the url input does not start with a protocol and the string does not contain a `.`
- Default to `https` over `http`
- Desktop notifications for download- and javascript-status
- Disable GTK window decorations.
    - This is temporary until [#2191](https://gitlab.gnome.org/GNOME/gtk/-/merge_requests/2191) is merged.

See manpage for all features, variables and external program usuage

## Examples of external program use
A basic `cgullhistory` in posix shell might look like
```
     #!/bin/sh
     tac "$CGULL_HISTORY_FILE" | dmenu | xargs cgull
```
Similarly, `cgullbookmarks`
```
     #!/bin/sh
     cat "$HOME/.cache/cgull/bookmarks" | dmenu | xargs cgull
```
The file "bookmarks" contains a list of links,
because it is an external program, you can make this as complex as you like.
You can even give the bookmarks names and output the corresponding url into cgull.

`cgullexternalhander` works a bit different,
it receives the current url as $1, so you might use
```
   #!/bin/sh
   firefox $1
```
to open the link in firefox, though you probably want to make a selection menu with something like dmenu
```
   #!/bin/sh
   echo "firefox\nvhromium\nmpv\nyoutube-dl" | dmenu | xargs cgull $1
```

For each of these examples, one should remember that the scripts are just that, **examples**.
Primarily, they do not check if the user actually selects anything,
thus always opening a new tab on cgull even if no bookmark or history-url was selected.

Better examples can be found under `user-scripts/`

## Installation
The following C libraries are required:

- GTK+ 3
- WebKit2 API for GTK+ 3
- Libnotify

cgull expects to be run on a POSIX-ish operating system.

To build the program and install it to /usr/local:

    $ make
    # make install

To use bundled web extensions, they must be copied or symlinked to the
appropriate path. Please refer to the manpage.


## Running
You simply invoke the main program:

    $ cgull

Refer to the manpage for all options.

## Background information
What cgull is and what it's not
cgull does what I need. It won't do other things.
cgull does not compete with powerful browsers like dwb or luakit, nor
with monstrous applications like Firefox or Chromium. 

About the name,
"cgull" deconstructs into "C-GTK-User's-Lariza".
Lariza is of course the original browser this fork is based on,
written in c with GTK.
User is me.
