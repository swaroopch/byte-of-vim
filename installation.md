# Installation

Let's see how to get Vim installed on your computer.

## Windows

If you use Microsoft Windows, then the following steps will help you get the latest version of Vim 7 installed on your computer:

1. Visit http://www.vim.org/download.php#pc
2. Download the "Self-installing executable" (gvim72.exe [1] as of this writing)
3. Double-click the file and install Vim like any other Windows-based software.

## Mac OS X

If you use Mac OS X, then you already have the terminal version of Vim installed. Run the menu command Finder &rarr; Applications &rarr; Utilities &rarr; Terminal. In the terminal, run the command vim and press enter, you should now see the Vim welcome screen.

If you want to use a graphical version of Vim, download the latest version of the [Cocoa-based MacVim project](http://code.google.com/p/macvim/). Double-click the file (such as `MacVim-7_2-stable-1_2.tbz`), it will be unarchived and a directory called `MacVim-7_2-stable-1_2` will be created. Open the directory, and copy the MacVim app to your Applications directory.

For more details MacVim diffrences, including how to run MacVim from the terminal see the macvim reference:

1. Click on Finder &rarr; Applications &rarr; MacVim.
2. Type :help macvim and press the Enter key.

## Linux / BSD

If you are using a Linux or *BSD system, then you will have at least a minimal console version of Vim already installed. Open a terminal program such as `konsole` or `gnome-terminal`, run `vim` and you should see the Vim welcome screen.

If you get a message like `vim: command not found`, then Vim is not installed. You will have to use your system-specific tools to install Vim, such as aptitude in Ubuntu/Debian Linux, yum in Fedora Linux, pkg_add or port in FreeBSD, etc. Please consult your specific system's documentation and forums on how to install new packages.

If you want the graphical version, install the vim-gnome package or alternatively, the gvim package.

## Summary


Depending on how it is installed, you can run the `vim` command in the shell or use your operating system's menus to open a graphical version of the Vim application.

Now that we have Vim installed on your computer, let us proceed to use it in the next chapter.
