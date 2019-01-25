# NAME
`passtyper` - a simple [dmenu](http://tools.suckless.org/dmenu/)-based client for [pass](https://www.passwordstore.org/)

## SYNOPSIS
```
passtyper [ OPTIONS ] [ -- dmenu arguments ]
```

## DESCRIPTION

`passtyper` is a client for [pass](https://www.passwordstore.org/) I wrote in a few hours because none of the existing clients suited my usecase exactly. It uses `xdotool` for autotyping password, username, or the combination of username and password separated by a configurable character. This character defaults to tab for compability with most web login forms, but can also be set to `\n`, `:`, or other printable characters for compatibility with other forms of entry.

Alternatively, `passtyper` supports writing one or both of the fields to the clipboard instead, using the same mechanism pass uses, which respects `PASSWORD_STORE_CLIP_TIME` and defaults to 45 seconds. The main usecase for this is a form that does not adhere to the expected sequence of `<username>` `<tab>` `<password>`, in which case the safest option is to autotype the password and paste the username from clipboard.

`passtyper` uses a few mechanisms to automatically retrieve the username from a pass entry:

1. Search the metadata for a line beginning with "username: " (not case sensitive).
If found, return the remainder of the line as username.
2. Use the first line of the metadata, unless that line contains a ` ` or `:`.
3. Use the environment variable `FALLBACKUSER` if set to a non-empty string.
4. Use the basename of the pass entry with a configurable suffix set in `FALLBACKUSERSUFFIX`, which is useful if you are in the habit of using <websitename>@<yourdomain>.example.

Password selection is done through `dmenu`.

If no options are given, `passtyper` defaults to autotyping the password.


## OPTIONS

Option parsing is done using `getopt`. Long options may be abbreviated as long as the abbreviation is unambiguous. Option arguments must either be their starting character or the entire argument (type may also be provided as t, clipboard as c, none as n).

`-p[t|c|n]`, `--password[=type|clipboard|none]`: Control the behaviour of password output: type it, copy it to clipboard, or suppress the password. Defaults to `type`.

`-u[t|c|n]`, `--username[=type|clipboard|none]`: Control the behaviour of username output: type it, copy it to clipboard, or suppress the username. By default `passtyper` does not output usernames. If the argument to --username is omitted, it uses `type`.

`-s'CHAR'`, `--separator='CHAR'`: Use a different separator for the concatenation of username and password. Newlines (`\n`), tabs (`\t`) and all printable characters are supported. Defaults to a tab (`\t`).

## CONFIGURATION
The file `${XDG_CONFIG_HOME}/passtyper/config` (default `$HOME/.config/passtyper/config`) is sourced automatically if present. Set `FALLBACKUSER` or `FALLBACKUSERSUFFIX` here.

## DEPENDENCIES

[pass](https://www.passwordstore.org/) (duh)

[dmenu](http://tools.suckless.org/dmenu/) (or something providing dmenu, such as [rofi](https://github.com/DaveDavenport/rofi) (untested))

[xdotool](http://www.semicomplete.com/projects/xdotool/) for autotype-support.

[xclip](https://github.com/astrand/xclip) for clipboard-support.

## AUTHOR & COPYRIGHT & LEGAL
The `clip()` function was written by Jason A. Donenfeld of zx2c4.com and [is licensed under the MIT license](https://xn--4db.cc/MzwCY38c/bash), text of which is included below. Apologies for the part where the license shouts at you.

The rest of passtyper was (badly) written in a few hours by Pol Van Aubel and licensed under [CC0](https://creativecommons.org/publicdomain/zero/1.0/). I don't care what you do with my code, just don't rip off Jason's.

Use of passtyper is at your own risk, and the author will not accept liability for it dumping your password into IRC channels, shady websites, command line history, process listings, or other screw-ups. Read the code, it's just string juggling.

## MIT LICENSE TEXT APPLICABLE TO CLIP()
Copyright (c) 2018 Jason A. Donenfeld

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

