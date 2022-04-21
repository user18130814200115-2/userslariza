<p align="center">
    <img width="200" src="cgull.svg" alt="Material Bread logo" align="center">
</p>
<h1 align="center">Cgull browser</h1>
<p align="center">
    Cgull is a simple webkit2gtk browser which focuses on simplicity and extensibility.
    <br>
    Cgull supports tabs, interaction with external programs (more accurately shell scripts) as well as JavaScript-,
    and Webkit-based extensions.
</p><p align="center">
    The project is originally forked from the <a href="https://uninformativ.de/git/lariza">lariza browser</a>.
</p>

## Features
- Multi functional input box for websearch, url's and page search.
- Built-in download manager
- Indicator for web feeds and JavaScript
- Global content zoom
- Cooperative instances using FIFOs
- Certificate trust store
- Bundled user-supplied JavaScripts (optional):
    - Link hints
    - Reader mode
- Bundled web extensions (optional):
    - Adblock
- Integration with external programs for:
    - history
    - bookmarks
    - native viewers (pdf, mp4, etc.)
- Keybindings for nearly every action
- HTTPS by default
- Manpage documentation

Cgull does not have a config file, changes can be made by editing the source code and a few variables are read from the environment.

See the manpages for all features, variables and external program usage.

## Examples of external program use
Cgull uses a script called `cgullexternalhandler` which may be written in any language and is passed the current 
uri when called.

To explain the power of the external handler script, you can look at the example provided `user-scripts/`.
The script in that folder opens a dmenu-like selection menu with options to:

- Open Link in mpv
  - for opening YouTube videos in a local player
- Get and type a TOTP
  -  Looks at the url and fetches the appropriate OTP code from pass, then types it out.
- Add a Bookmark
  - add the current url to the bookmarks file
- Open link in reddit viewer
  - open the current page in a terminal window running tuir (for reddit pages)
- Format page as pdf
  - Formats the current page into a nicely readable pdf

You can of course also forgo the selection menu and simply write a script like:
```
firefox "$1"
```
To open the provided link in firefox.

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
