# More
## Introduction
We've explored so many features of Vim, but we still haven't covered them all, so let's take a quick wild ride through various topics that are useful and fun.

## Modeline
What if you wanted to specify that a certain file should always use pure tabs and no spaces while editing. Can we enforce that within the file itself?

Yes. Just put `vim: noexpandtab` within the first two lines or last two lines of your file.

An example:
```
# Sample Makefile
.cpp:
    $(CXX) $(CXXFLAGS) $< -o $@

# vim: noexpandtab
```
This line we are adding is called a "modeline."

## Portable Vim
If you keep switching between different computers, isn't it a pain to maintain your Vim setup exactly the same on each machine? Wouldn't it useful if you could just carry Vim around in your own USB disk? This is exactly what [Portable GVim](http://portablegvim.sourceforge.net) is.

Just unzip into a directory on the portable disk, then run `GVimPortable.exe`. You can even store your own `vimrc` and other related files on the disk and use it anywhere you have a Microsoft Windows computer.

## Upgrade plugins
Any sufficiently advanced Vim user would be using a bunch of plugins and scripts added to their `~/.vim` or `~/vimfiles` directory. What if we wanted to update them all to the latest versions? You could visit the script page for each of them, download and install them, but there's a better way: just run `:GLVS` (which stands for 'G'et 'L'atest 'V'im 'S'cripts).

See `:help getscript` for details.

There are scripts to even [twitter from Vim](http://www.vim.org/scripts/script.php?script_id=1853)!

## Dr.Chip's plugins
"Dr. Chip" has written some [amazing Vim plugins](http://www.drchip.org/astronaut/vim/) over many years.

One of my favorites is [drawit.vim](http://www.vim.org/scripts/script.php?script_id=40), which helps you to draw text-based drawings such as those fancy ASCII diagrams you have seen before.

Another is [align.vim](http://www.vim.org/scripts/script.php?script_id=294), which helps you to align consecutive lines together. For example, say you have the following piece of program code:
```
a = 1
bbbbb = 2
cccccccccc = 3
```
Just visually select these three lines and press \t=, and voila, it becomes like this:
```
a          = 1
bbbbb      = 2
cccccccccc = 3
```
This is much easier to read than before and makes your code look more professional. Explore Dr. Chip's page to find out about many more interesting plugins.

## Blog from Vim
Using the [Vimpress plugin](http://www.vim.org/scripts/script.php?script_id=1953), you can blog to your Wordpress blog right within Vim.

## Make Firefox work like Vim
Use the [Vimperator add-on](http://vimperator.mozdev.org/) to make Firefox behave like Vim, complete with modal behavior, keyboard shortcuts to visit links, status line, tab completion, and even marks support!

## Bram's talk on the seven habits
Bram Moolenaar, the creator of Vim, had written an article long ago titled ["Seven habits of effective text editing"](http://www.moolenaar.net/habits.html) that explained how you should use a good editor (such as Vim).

Bram recently gave a talk titled ["Seven habits for effective text editing, 2.0"](https://youtu.be/eX9m3g5J-XA) where he goes on to describe the newer features of Vim as well as how to effectively use Vim. This talk is a good listen for any regular Vim user.

## Contribute to Vim
You can contribute to Vim in various ways, such as working on [development of Vim itself](http://groups.google.com/group/vim_dev), [writing plugins and color schemes](http://www.vim.org/scripts/), [contributing tips](http://vim.wikia.com), and [helping with the documentation](http://vimdoc.sourceforge.net).

If you want to help in the development of Vim itself, see `:help development`.

## Community
Many Vim users hang out at the [vim@vim.org mailing list](http://www.vim.org/maillist.php#vim) where questions and doubts are asked and answered. The best way to learn more about Vim and to help other beginners learn Vim is to frequently read (and reply) to emails in this mailing list.

Find more articles and discussions at [Google+](https://plus.google.com/communities/105049811056605918816) and [reddit](http://www.reddit.com/r/vim/).

## Summary
We've seen some wide range of Vim-related stuff and how it can be beneficial to us. Feel free to explore these and many more [Vim scripts](http://www.vim.org/scripts/) to help you ease your editing and make it even more convenient.
