```
   _            _
  | | __ _ _ __(_)______ _
  | |/ _` | '__| |_  / _` |
  | | (_| | |  | |/ / (_| |
  |_|\__,_|_|  |_/___\__,_|
```  
 
  https://uninformativ.de/git/lariza
  https://uninformativ.de/bugs.html


- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

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
  - Pressing this keybinding will load `larizahistory` from your PATH
- Keybind for `larizabookmarks` external program simmilar to `larizahistory`, may be integrated with `larizaexternalhandler`
- Brought back `larizaexternalhandler`
  - This is a language agnostic program that is called on Ctrl+Shift+o by default.
  - The program will be called like so `larizaexternalhandler $CURRENT_URL` to open the current url in the bar with an external program
- A lariza.desktop file is automatically installed on `make install`
- Keys for previous/next tab remapped to (ctrl+Left) (ctrl+Right)
- Dedicated keys to get to a certain tab on (ctrl+`n`) where `n` is a number key
- Search duckduckgo if the url input does not start with a protocol and the string does not conatin a `.`
   - EG typing `test` into the urlbar will lead to `https://duckduckgo.com/html?q=test` while `test.com` will default to `https://test.com`
- Default to `https` over `http`
- Instead of opening up the download manager when a new download is started, send a desktop notification
   - Download manager is still accessible through the keybind  

## Examples of external program use
A basic larizahistory is posix shell might look like
```
     #!/bin/sh
     tac "$LARIZA_HISTORY_FILE" | dmenu | xargs lariza
```
Similarly, `larizabookmarks`
```
     #!/bin/sh
     cat "$HOME/.cache/lariza/bookmarks" | dmenu | xargs lariza
```
The file "bookmarks" contains a list of links,
because it is an external program, you can make this as complex as you like.
You can even give the bookmarks names and output the corresponding url into lariza.

`larizaexternalhander` works a bit different,
it receives the current url as $1, so you might use
```
   #!/bin/sh
   firefox $1
```
to open the link in firefox, though you probably want to make a selection menu with something like dmenu
```
   #!/bin/sh
   echo "firefox\nvhromium\nmpv\nyoutube-dl" | dmenu | xargs lariza $1
```

For each of these examples, one should remember that the scripts are just that, **examples**.
Primarily, they do not check if the user actually selects anything,
thus always opening a new tab on lariza even if no bookmark or history-url was selected.

Better examples can be found under `user-scripts/`

## Installation
The following C libraries are required:

- GTK+ 3
- WebKit2 API for GTK+ 3
- Libnotify

lariza expects to be run on a POSIX-ish operating system.

To build the program and install it to /usr/local:

    $ make
    # make install

To use bundled web extensions, they must be copied or symlinked to the
appropriate path. Please refer to the manpage.


## Running
You simply invoke the main program:

    $ lariza

Refer to the manpage for all options.

## Note on the manpage
The manpage ahs not been edited for use with this fork,
proceed with caution.

## Background information
What lariza is and what it's not
lariza does what I need. It won't do other things. I'm open for pull
requests but please don't be upset if I turn them down -- which might
happen if it's a feature that I simply don't need. That being said,
you should have a look at the PATCHES file. :-)
lariza does not compete with powerful browsers like dwb or luakit, nor
with monstrous applications like Firefox or Chromium. 

About the name
"lariza" stems from a german sentence:
```
Alle anderen waren mir zu anstrengend.
 l   a         r    i  z  a
```
That phrase basically means: "It was too tiresome to deal with any
other browser." I couldn't find a simple browser that does just what I
need. Most of them are utterly bloated, others lack essential
functions. Thus, I was forced to write scripts and tools and stuff to
deal with these issues. That is what was tiresome. I don't want to
work around bugs or nonsensical behavior anymore.
So, I wrote my own browser^W WebKit GUI. WebKit does all the dirty
work.

