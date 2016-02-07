# Plugins

As we have seen in the previous chapter, we can write scripts to extend the existing functionality of Vim to do more stuff. We call these scripts which extend or add functionality as "plugins."

There are various kinds of plugins that can be written:

- vimrc
- global plugin
- filetype plugin
- syntax highlighting plugin
- compiler plugin

Not only can you write your own plugins but also download and [use plugins written by others](http://www.vim.org/scripts/index.php).

## Customization using vimrc

When I install a new Linux distribution or reinstall Windows, the first thing I do after installing Vim is fetch my latest `vimrc` file from my backups, and then start using Vim. Why is this important? Because the `vimrc` file contains various customizations/settings I like which makes Vim more useful and comfortable for me.

There are two files you can create to customize Vim to your taste:

1. vimrc - for general customizations
2. gvimrc - for GUI specific customizations

These are stored as:

- `%HOME%/_vimrc` and `%HOME%/_gvimrc` on Windows
- `$HOME/.vimrc` and `$HOME/.gvimrc` on Linux/BSD/Mac OS X

See `:help vimrc` on the exact location on your system.

These vimrc and gvimrc files can contain any Vim commands. The convention followed is to use only simple settings in the vimrc files, and advanced stuff are sourced from plugins.

For example, here's a portion of my vimrc file:

``` viml
" My Vimrc file
" Maintainer: www.swaroopch.com/contact/
" Reference: Initially based on http://dev.gentoo.org/~ciaranm/docs/vim-guide/
" License: www.opensource.org/licenses/bsd-license.php

" Use Vim settings, rather then Vi settings (much better!).
" This must be first, because it changes other options as a side effect.
set nocompatible


" Enable syntax highlighting.
syntax on

" Automatically indent when adding a curly bracket, etc.
set smartindent

" Tabs should be converted to a group of 4 spaces.
" This is the official Python convention
" http://www.python.org/dev/peps/pep-0008/
" I didn't find a good reason to not use it everywhere.
set shiftwidth=4
set tabstop=4
set expandtab
set smarttab

" Minimal number of screen lines to keep above and below the cursor.
set scrolloff=999

" Use UTF-8.
set encoding=utf-8

" Set color scheme that I like.
if has("gui_running")
  colorscheme desert
else
  colorscheme darkblue
endif

" Status line
set laststatus=2
set statusline=
set statusline+=%-3.3n\                      " buffer number
set statusline+=%f\                          " filename
set statusline+=%h%m%r%w                     " status flags
set statusline+=\[%{strlen(&ft)?&ft:'none'}] " file type
set statusline+=%=                           " right align remainder
set statusline+=0x%-8B                       " character value
set statusline+=%-14(%l,%c%V%)               " line, character
set statusline+=%<%P                         " file position

" Show line number, cursor position.
set ruler

" Display incomplete commands.
set showcmd

" To insert timestamp, press F3.
nmap <F3> a<C-R>=strftime("%Y-%m-%d %a %I:%M %p")<CR><Esc>
imap <F3> <C-R>=strftime("%Y-%m-%d %a %I:%M %p")<CR>

" To save, press ctrl-s.
nmap <c-s> :w<CR>
imap <c-s> <Esc>:w<CR>a

" Search as you type.
set incsearch

" Ignore case when searching.
set ignorecase

" Show autocomplete menus.
set wildmenu

" Show editing mode
set showmode

" Error bells are displayed visually.
set visualbell
```

Notice that these commands are not prefixed by colon. The colon is optional when writing scripts in files because it assumes they are normal mode commands.

If you want to learn detailed usage of each setting mentioned above, refer `:help`.

A portion of my gvimrc file is:

``` viml
" Size of GVim window
set lines=35 columns=99

" Don't display the menu or toolbar. Just the screen.
set guioptions-=m
set guioptions-=T

" Font.
if has('win32') || has('win64')
  " set guifont=Monaco:h16
  " http://jeffmilner.com/index.php/2005/07/30/windows-vista-fonts-now-available/
  set guifont=Consolas:h12:cANSI
elseif has('unix')
  let &guifont="Monospace 10"
endif
```

There are various example vimrc files out there that you should definitely take a look at and learn the various kinds of customizations that can be done, then pick the ones you like and put it in your own vimrc.

A few good ones that I have found in the past are:

- [Steve Francia's vim distribution](http://vim.spf13.com)
- [Steve Losh's vim config](http://stevelosh.com/blog/2010/09/coming-home-to-vim/)
- [bling's dotvim](https://github.com/bling/dotvim)
- [Janus](https://github.com/carlhuda/janus)

It is a known fact that a person's vimrc usually reflects how long that person has been using Vim.

## Global plugin

Global plugins can be used to provide global/generic functionality.

Global plugins can be stored in two places:

1. `$VIMRUNTIME/plugin/` for standard plugins supplied by Vim during its installation
2. To install your own plugins or plugins that you have download from somewhere, you can use your own plugin directory:

    - `$HOME/.vim/plugin/` on Linux/BSD/Mac OS X
    - `%HOME%/vimfiles/plugin/` on Windows
    - See `:help runtimepath` for details on your plugin directories.

Let's see how to use a plugin.

A useful plugin to have is [`highlight_current_line.vim`](http://www.vim.org/scripts/script.php?script_id=1652) by Ansuman Mohanty which does exactly as the name suggests. Download the latest version of the file `highlight_current_line.vim` and put it in your plugin directory (as mentioned above). Now, restart Vim and open any file. Notice how the current line is highlighted compared to the other lines in the file.

But what if you don't like it? Just delete the `highlight_current_line.vim` file and restart Vim.

Similarly, we can install our own `related.vim` or `capitalize.vim` from the Scripting chapter into our plugin directory, and this avoids us the trouble of having to use :source every time. Ultimately, any kind of Vim plugin that you write should end up somewhere in your `.vim/vimfiles` plugin directory.

## Filetype plugin

Filetype plugins are written to work on certain kinds of files. For example, programs written in the C programming language can have their own style of indentation, folding, syntax highlighting and even error display. These plugins are not general purpose, they work for these specific filetypes.

### Using a filetype plugin

Let's try a filetype plugin for XML. XML is a declarative language that uses tags to describe the structure of the document itself. For example, if you have a text like this:

> Iron Gods <br>
> ---------  <br>
> <br>
> Ashok Banker's next book immediately following the Ramayana is said to be a novel tentatively titled "Iron Gods" scheduled to be published in 2007. A contemporary novel, it is an epic hard science fiction story about a war between the gods of different faiths. Weary of the constant infighting between religious sects and their deities, God (aka Allah, Yahweh, brahman, or whatever one chooses to call the Supreme Deity) wishes to destroy creation altogether. <br>
> <br>
> A representation of prophets and holy warriors led by Ganesa, the elephant-headed Hindu deity, randomly picks a sample of mortals, five of whom are the main protagonists of the book--an American Catholic, an Indian Hindu, a Pakistani Muslim, a Japanese Buddhist, and a Japanese Shinto follower. The mortal sampling, called a 'Palimpsest' is ferried aboard a vast Dyson's Sphere artifact termed The Jewel, which is built around the sun itself, contains retransplanted cities and landscapes brought from multiple parallel Earths and is the size of 12,000 Earths. It is also a spaceship travelling to the end of creation, where the Palimpsest is to present itself before God to plead clemency for all creation. <br>
> <br>
> Meanwhile, it is upto the five protagonists, aided by Ganesa and a few concerned individuals, including Lucifer Morningstar, Ali Abu Tarab, King David and his son Solomon, and others, to bring about peace among the myriad warring faiths. The question is whether or not they can do so before the audience with God, and if they can do so peacefully--for pressure is mounting to wage one final War of Wars to end all war itself.

(Excerpt taken from [Wikipedia](http://en.wikipedia.org/w/index.php?title=Ashok_Banker&oldid=86219280) under the GNU Free Documentation License)

It can be written in XML form (specifically, in 'DocBook XML' format) as:
