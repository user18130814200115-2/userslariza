# Cgull browser
This is a fork of the [lariza browser](https://uninformativ.de/git/lariza),
a simple webkit GTK3 browser.

## Regular features
- A WebKit2 viewport
- An input box to change the URI or to search the current page
- Built-in download manager
- Indicator for web feeds
- Global content zoom
- Cooperative instances using FIFOs
- Certificate trust store
- Bundled user-supplied JavaScripts (optional):
    - Link hints
- Bundled web extensions (optional):
    - Adblock

## Added features
- Keybindings to disable- (ctl+j) and re-enable-javascript (ctrl+shift+j)
- Keybindings added for zooming in and out (ctrl+=) (ctrl+-)
  + Keybind to reset zoom (ctrl+0)
- Other keybindings have been changed to be more familiar
    - Search moved to ctrl+f
    - Main mod key moved from Mod1 to ctrl
- Keybinding to manage history with external program (ctrl+h)
  - Pressing this keybinding will load `cgullhistory` from your PATH
- Keybind for `cgullbookmarks` external program simmilar to `cgullhistory`, may be integrated with `cgullexternalhandler`
- Brought back `larizaexternalhandler` in the form of `cgullexternalhandler`
  - This is a language agnostic program that is called on Ctrl+Shift+o by default.
  - The program will be called like so `cgullexternalhandler $CURRENT_URL` to open the current url in the bar with an external program
- A cgull.desktop file is automatically installed on `make install`
- Keys for previous/next tab remapped to (ctrl+Left) (ctrl+Right)
- Dedicated keys to get to a certain tab on (ctrl+`n`) where `n` is a number key
- Search CGULL_SEARCH_URI if the url input does not start with a protocol and the string does not contain a `.`
   - CGULL_SEARCH_URI defaults to `https://html.duckduckgo.com/html`
   - EG typing `test` into the urlbar will lead to `https://html.duckduckgo.com/html?q=test` while `test.com` will default to `https://test.com`
- Default to `https` over `http`
- Instead of opening up the download manager when a new download is started, send a desktop notification
   - Download manager is still accessible through the keybind  
- Disable GTK window decorations.
    - This is temporary until [#2191](https://gitlab.gnome.org/GNOME/gtk/-/merge_requests/2191) is merged.

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
cgull does what I need. It won't do other things. I'm open for pull
requests but please don't be upset if I turn them down -- which might
happen if it's a feature that I simply don't need. That being said,
you should have a look at the PATCHES file. :-)
cgull does not compete with powerful browsers like dwb or luakit, nor
with monstrous applications like Firefox or Chromium. 

About the name,
"cgull" deconstructs into "C-GTK-User's-Lariza".
Lariza is of course the original browser this fork is based on,
written in c with GTK.
User is me.
