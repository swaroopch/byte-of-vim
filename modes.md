# Modes

We had our first encounter with modes in the previous chapter. Now, let us explore this concept further regarding types of modes available and what we can do in each mode.

## Types of modes

There are three basic modes in Vim:

1. Normal mode is where you can run commands. This is the default mode in which Vim starts up.
2. Insert mode is where you insert i.e. write the text.
3. Visual mode is where you visually select a bunch of text so that you can run a command/operation only on that part of the text.

## Normal mode

By default, you're in normal mode. Let's see what we can do in this mode.

Type `:echo "hello world"` and press enter. You should see the famous words hello world echoed back to you. What you just did was run a Vim command called `:echo` and you supplied some text to it which was promptly printed back.

Type `/hello` and press the enter key. Vim will search for that phrase and will jump to the first occurrence.

This was just two simple examples of the kind of commands available in the normal mode. We will see many more such commands in later chapters.

## How to use the help

Almost as important as knowing the normal mode, is knowing how to use the `:help` command. This is where you learn more about the commands available in Vim.

Remember that you do not need to know every command available in Vim, it's better to simply know where to find them when you need them. For example, see `:help usr_toc` takes us to the table of contents of the reference manual. You can see `:help index` to search for the particular topic you are interested in, for example, run `/insert mode` to see the relevant information regarding insert mode.

If you can't remember these two help topics at first, just press `F1` or run `:help`.

## Insert mode

When Vim starts up in normal mode, we have seen how to use i to get into insert mode. There are other ways of switching from normal mode to insert mode as well:

1. Run `:e dapping.txt`
2. Press `i`
3. Type the following paragraph (including all the typos and mistakes, we'll correct them later):

    > means being determined about being determined and being passionate about being passionate

4. Press `<Esc>` key to switch back to normal mode.
5. Run `:w`

Oops, we seem to have missed a word at the beginning of the line, and our cursor is at the end of the line, what do we do now?

What would be the most efficient way of going to the start of the line and insert the missing word? Should we use the mouse to move the cursor to the start of the line? Should we use arrow keys to travel all the way to the start of the line. Should we press home key and then press i to switch back to insert mode again?

It turns out that the most efficient way to be press `I` (upper case I):

1. Press `I`
2. Type `Dappin`
3. Press `<Esc>` key to switch back to the normal mode.

Notice that we used a different key to switch to insert mode, its specialty is that it moves the cursor to the start of the line and then switches to the insert mode.

Also notice how important it is to *switch back to the normal mode as soon as you're done typing the text*. Making this a habit will be beneficial because most of your work (after the initial writing phase) will be in the normal mode - that's where the all-important rewriting/editing/polishing happens.

Now, let's take a different variation of the `i` command. Notice that pressing `i` will place your cursor before the current position and then switch to insert mode. To place the cursor 'a'fter the current position, press `a`.

1. Press `a`
2. Type `g` (to complete the word as "Dapping")
3. Press `<Esc>` to switch back to normal mode

Similar to the relationship between `i` and `I` keys, there is a relationship between the `a` and `A` keys - if you want to append text at the end of the line, press the `A` key.

1. Press `A`
2. Type `.` (put a dot to complete the sentence properly)
3. Press `<Esc>` to switch back to the normal mode

To summarize the four keys we have learnt so far:

| Command | Action |
| --- | --- |
| `i` | insert text just before the cursor |
| `I` | insert text at the start of the line |
| `a` | append text just after the cursor |
| `A` | append text at the end of the line |

Notice how the upper case commands are 'bigger' versions of the lower case commands.

Now that we are proficient in quickly moving in the current line, let's see how to move to new lines. If you want to 'o'pen a new line to start writing, press the `o` key.

1. Press `o`
2. Type `I'm a rapper`.
3. Press `<Esc>` to switch back to the normal mode.

Hmmm, it would be more appealing if that new sentence we wrote was in a paragraph by itself.

1. Press `O` (upper case 'O')
2. Press `<Esc>` to switch back to the normal mode.

To summarize the two new keys we just learnt:

| Command | Action | 
| --- | --- |
| `o` | open a new line below |
| `O` | open a new line above |

Notice how the upper and lower case 'o' commands are opposite in the direction in which they open the line.

Was there something wrong in the text that we just wrote? Aah, it should be 'dapper', not 'rapper'! It's a single character that we have to change, what's the most efficient way to make this change?

We could press `i` to switch to insert mode, press `<Del>` key to delete the `r`, type `d` and then press `<Esc>` to switch back to the insert mode. But that is four steps for such a simple change! Is there something better? You can use the `s` key - s for 's'ubstitute.

1. Move the cursor to the character `r` (or simply press `b` to move 'b'ack to the start of the word)
2. Press `s`
3. Type `d`
4. Press `<Esc>` to switch back to the normal mode

Well, okay, it may not have saved us much right now, but imagine repeating such a process over and over again throughout the day! Making such a mundane operation as fast as possible is beneficial because it helps us focus our energies to more creative and interesting aspects. As Linus Torvalds says, *"it's not just doing things faster, but because it is so fast, the way you work dramatically changes."*

Again, there is a bigger version of the `s` key, `S` which substitutes the whole line instead of the current character.

1. Press `S`
2. Type `Be a sinner`.
3. Press `<Esc>` to switch back to normal mode.

| Command | Action | 
| --- | --- |
| `s` | substitute the current character |
| `S` | substitute the current line |

Let's go back our last action... Can't we make it more efficient since we want to 'r'eplace just a single character? Yes, we can use the `r` key.

1. Move the cursor to the first character of the word `sinner`.
2. Press `r`
3. Type `d`

Notice we're already back in the normal mode and didn't need to press `<Esc>`.

There's a bigger version of `r` called `R` which will replace continuous characters.

1. Move the cursor to the 'i' in sinner.
2. Press `R`
3. Type `app` (the word now becomes 'dapper')
4. Press `<Esc>` to switch back to normal mode.

| Command | Action | 
| --- | --- |
| `r` | replace the current character |
| `R` | replace continuous characters |

The text should now look like this:

> Dapping means being determined about being determined and being passionate about being passionate.
> <br>
> Be a dapper.

Phew. We have covered a lot in this chapter, but I guarantee that this is the only step that is the hardest. Once you understand this, you've pretty much understood the heart and soul of how Vim works, and all other functionality in Vim, is just icing on the cake.

To repeat, understanding how modes work and how switching between modes work is the key to becoming a Vimmer, so if you haven't digested the above examples yet, please feel free to read them again. Take all the time you need.

If you want to read more specific details about these commands, see `:help inserting` and `:help replacing`.

## Visual mode

Suppose that you want to select a bunch of words and replace them completely with some new text that you want to write. What do you do?

One way would be to use the mouse to click at the start of the text that you are interested in, hold down the left mouse button, drag the mouse till the end of the relevant text and then release the left mouse button. This seems like an awful lot of distraction.

We could use the `<Del>` or `<Backspace>` keys to delete all the characters, but this seems even worse in efficiency.

The most efficient way would be to position the cursor at the start of the text, press v to start the visual mode, use arrow keys or any text movement commands to the move to the end of the relevant text (for example, press `5e` to move to the end of the 5th word counted from the current cursor position) and then press `c` to 'c'hange the text. Notice the improvement in efficiency.

In this particular operation (the `c` command), you'll be put into insert mode after it is over, so press `<Esc>` to return to normal mode.

The `v` command works on a character basis. If you want to operate in terms of lines, use the upper case `V`.

## Summary

Here is a drawing of the relationship between the different modes:

```
+---------+  i,I,a,A,o,O,r,R,s,S  +----------+
| Normal  +---------->------------+ Insert   |
| mode    |                       | mode     |
|         +----------<------------+          |
+-+---+---+        <Esc>          +----------+
   |  |
   |  |
   |  |
   |  |
v, |  |
V  V  ^ <Esc>
   |  |
   |  |
   |  |
   |  |
+---+---+----+
| Visual     |
| mode       |
+------------+
```

> NOTE: This drawing was created using Vim and [Dr.Chip's DrawIt plugin](http://www.vim.org/scripts/script.php?script_id=40).

See `:help vim-modes-intro` and `:help mode-switching` for details on the various modes and how to switch between them respectively.

If you remain unconvinced about why the concept of modes is central to Vim's power and simplicity, do read the articles on ["Why Vi"](http://www.viemu.com/a-why-vi-vim.html) and about the [vi input model](http://blog.ngedit.com/2005/06/03/the-vi-input-model/) on why it is a better way of editing.
