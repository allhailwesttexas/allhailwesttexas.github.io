---
title: Setting Up a Python Development Environment on Windows
layout: post
---

Getting started with Python and looking for a good setup? Or maybe experienced
Python-person looking to look down on someone else's inferior setup? Either
way, this might be the page for you! Here I'll describe my general setup for
writing world-changing software such as [Todo for
Windows](http://www.github.com/allhailwesttexas/todo). I originally wrote it
after setting up the same environment on three of my co-workers' computers -
like any good programmer, I'm lazy and try my best to "automate" everything (in
this case, "automate" just means "make someone else do it instead of me").

##Editor

I like [Sublime Text 3](http://www.sublimetext.com/3). It is technically in
beta, but works very well. It costs about $60, but has a free version that
very occasionally nags you to buy. I bought it after a while because I thought
it was really good. Get it.

Then install [Package Control](https://sublime.wbond.net/installation#st3). It
looks a bit daunting, but all you have to do is paste some text into the
Sublime command prompt (accessed with ``ctrl+` ``). Then we get an excellent
package management system, which is easily accessed with `ctrl+shift+p`, start
typing "install package" until it comes up. Then you get a list of packages
available. Get these to start with:

- SublimeCodeIntel (gives you autocomplete and clickable functions)
- SublimeLinter (gives you code linting - shows you any syntax errors you make)
- SublimeLinter-pyflakes (python-specific linting)
- AdvancedNewFile (`ctrl+alt+n` to easily create new files/folders)
- SidebarEnhancements (gives a better context menu when you right click on
sidebar items)
- Theme - Spacegray (just looks nicer)

There are a few other good ones too, have a look around. Most of these work out
of the box, but SublimeLinter needs a bit of extra work/love. You also have to
install the Python pyflakes package and make sure it is on your system `PATH`.
See the section on Python packages for details on how to do that.

Here are some things I like about Sublime Text:

- Easy access to all commands with `ctrl+shift+p`
- `ctrl+p` for easy switching between files
- `ctrl+click` to make multiple cursors
- `ctrl+D` to select next occurrence of a word/character
- `alt+f3` to select all occurrences
- `ctrl+l` to select lines, then `ctrl+shift+l` to make cursors on each line
- Making snippets
- Split panes (and other options) with `alt+shift+2`
- The find (`ctrl+shift+f`) functionality for all open files or all files in
directory
- Swapping lines with `ctrl+shift+up` or `down` arrow
- Pretty good (though far from perfect) vim bindings

Here is my `Settings (User)` file:

```javascript
{
    "auto_complete_commit_on_tab": true,
    "color_scheme": "Packages/User/base16-eighties.dark (SL).tmTheme",
    "detect_slow_plugins": true,
    "ensure_newline_at_eof_on_save": true,
    "find_selected_text": true,
    "fold_buttons": false,
    "font_face": "consolas",
    "font_size": 10,
    "highlight_line": false,
    "ignored_packages":
    [
    ],
    "rulers":
    [
        79
    ],
    "soda_classic_tabs": true,
    "soda_folder_icons": true,
    "spell_check": false,
    "theme": "Spacegray Eighties.sublime-theme",
    "translate_tabs_to_spaces": true,
    "trim_trailing_white_space_on_save": true,
    "vintage_start_in_command_mode": true,
    "word_wrap": false
}
```

##Source Control

I like [git](http://www.git-scm.com/) for source control. It's basically
standard these days, in large part due to [GitHub](https://www.github.com/).
Get it by installing [GitHub for Windows](http://windows.github.com/) which is
an easy to use (but somewhat limited in functionality - I still like it because
it's intuitive and very pretty) GUI for git.

GitHub is really good, but it's only free if all your code repositories are
public, which we can't always do. There's another site which is also quite
good, [BitBucket](https://www.bitbucket.org/), that allows you to have private
repositories for free. Get an account there. It is still possible to use the
GitHub for Windows app to push code to BitBucket.

##Python Packages

For packages, first see if it's available from
[here](http://www.lfd.uci.edu/~gohlke/pythonlibs/). If it's not, use `pip` to
install. To do this, download and install `pip` from the above site, then add
`C:\Python27\Scripts` to your `PATH` environment variable. You do this by
pressing the Windows key, starting to type "environment variable" until the
option "Change the system environment variables" comes up. Scroll to the `PATH`
variable and append `C:\Python27;C:\Python27\Scripts` to the end. Now you can
start a command line prompt and type `pip install <package>` and it will be
installed into your Python folder for future use in all your projects. If you
have SublimeLinter with Pyflakes installed, it should also work now. 

The reason we have to download precompiled installers for some packages is that
`pip` doesn't work on Windows for packages that have extensions written in C,
which practically all the scientific computing packages do. But for most things
it will work fine (`requests`, `click`, and so on).

The Python standard library is pretty extensive, and will have the tools to do
most things you will want to do. But, in many cases, someone else has written a
library that is easier to use and, well, more "Pythonic" (a word you will come
across here and there). Here are some of my go-to external libraries:

- [pandas](#) &ndash; If you do any scientific programming, this is where to start
- [click](#) &ndash; super-easy command-line interfaces (over `argparse`/`optparse`)
- [funcy](#) &ndash; intuitive, powerful manipulation of data structures and functions
- [requests](#) &ndash; the best way to make HTTP requests (over `urllib3`/`httplib`)
- [unipath](#) &ndash; file and folder path manipulation made easy (over `os.path`)

I use these all the time. They make Python much more enjoyable to write.
