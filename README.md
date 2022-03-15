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
    - Reader mode
- Bundled web extensions (optional):
    - Adblock
- Keybinding to toggle javascript
- Keybinding to hide the uri-, and tab-areas
- Keybinding to manage history and bookmarks with external program
    - Open the current link with an external program
- A cgull.desktop file is automatically installed on `make install`
- Dedicated keys to get to a certain tab on (ctrl+`n`) where `n` is a number key
- Search CGULL_SEARCH_URI if the url input does not start with a protocol and the string does not contain a `.`
- Default to `https` over `http`
- Desktop notifications for download status
- Disable GTK window decorations.
    - This is temporary until [#2191](https://gitlab.gnome.org/GNOME/gtk/-/merge_requests/2191) is merged.

See manpage for all features, variables and external program usuage

## Examples of external program use
Example scripts can be found under `user-scripts/`.

To explain the power of the external handler script,
here are some of the programs I have in there:

- mpv
  - for opening YouTube videos in a local player
- one time password
  -  Looks at the url and fetches the appropriate OTP code from pass, then types it out.
- bookmark
  - add the current url to the bookmarks file
- tuir
  - open the current page in a terminal window running tuir (for reddit pages)
- pdf format
  - Formats the current page into a nicely readable pdf similar to Firefox's reader mode


## Installation
The following C libraries are required:

- GTK+ 3
- WebKit2 API for GTK+ 3
- Libnotify

cgull expects to be run on a POSIX-ish operating system.

To build the program and install it to /usr/local:
```
$ make
# make install
```
To use bundled web extensions, they must be copied or symlinked to the
appropriate path. Please refer to the manpage.


## Running
You simply invoke the main program:
```
$ cgull
```
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
