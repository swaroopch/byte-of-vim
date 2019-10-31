# Editing Basics

Let's learn the basic editing commands in Vim for reading/writing files, cut/copy/paste, undo/redo and searching.

## Reading and writing files

### Buffers

When you edit a file, Vim brings the text in the file on the hard disk to the computer's RAM. This means that a copy of the file is stored in the computer's memory and any changes you make is changed in the computer's memory and immediately displayed. Once you have finished editing the file, you can save the file which means that Vim writes back the text in the computer's memory to the file on the hard disk. The computer memory used here to store the text temporarily is referred to as a "buffer". Note that this same concept is the reason why we have to "save" files in all editors or word processors that we use.

Now open up Vim, write the words `Hello World` and save it as the file `hello.txt`. If you need to remember how to do this, please refer to the [First Steps chapter](./first_steps.md#write-file).

### Swap

Now you will notice that another file has been created in the same directory as this file, the file would be named something like `.hello.txt.swp`. Run `:swapname` to find out the exact name of the file.

What is this file? Vim maintains a backup of the buffer in a file which it saves regularly to the hard disk so that in case something goes wrong (like a computer crash or even Vim crashes), you have a backup of the changes you have made since you last saved the original file. This file is called a "swap file" because Vim keeps swapping the contents of the buffer in the computer memory with the contents of this file on the hard disk. See `:help swap-file` to know more details.

### Save my file

Now that the file has been loaded, let's do a minor editing. Press the ~ key to change the case of the character on which the cursor is positioned. You will notice that Vim now marks the file having been changed (for example a `+` sign shows up in the title bar of the GUI version of Vim). You can open up the actual file in another editor and check that it has not changed yet i.e. Vim has only changed the buffer and not yet saved it to the hard disk.

We can write back the buffer to the original file in the hard disk by running `:write`.

> NOTE: To make saving easier, add the following line to your vimrc file:
> <br>
> ``` viml
> " To save, ctrl-s.
> nmap <c-s> :w<CR>
> imap <c-s> <Esc>:w<CR>a
> ```
> <br>
> Now you can simply press `ctrl-s` to save the file.

### Working in my directory

Vim starts up with your home directory as the default directory and all operations will be done within that directory.

To open files located in other directories, you can use the full or relative paths such as:

``` viml
:e ../tmp/test.txt
:e C:\\shopping\\monday.txt
```

Or you can switch Vim to that directory:

``` viml 
:cd ../tmp
```

`:cd` is short for 'c'hange 'd'irectory.

To find out the current directory where Vim is looking for files:

``` viml
:pwd
```

`:pwd` is short for 'p'rint 'w'orking 'd'irectory.

## Cut, Copy and Paste

As Sean Connery says, in the movie [Finding Forrester](http://www.imdb.com/title/tt0181536/):

> No thinking - that comes later. You must write your first draft with your heart. You rewrite with your head. The first key to writing is... to write, not to think!

When we rewrite, we frequently rearrange the order of the paragraphs or sentences i.e. we need to be able to cut/copy/paste the text. In Vim, we use a slightly different terminology:

| Desktop world | Vim world | Operation |
| --- | --- | --- |
| cut | delete | `d` |
| copy | yank | `y` | 
| paste | paste | `p` |

In normal desktop terminology, 'cut'ting text means removing the text and putting it into the clipboard. The same operation in Vim means it deletes the text from the file buffer and stores it in a 'register' (a part of the computer's memory). Since we can choose the register where we can store the text, it is referred to as the "delete" operation.

Similarly, in normal desktop terminology, 'copy' text means that a copy of the text is placed on the clipboard. Vim does the same, it "yanks" the text and places it in a register.

"Paste" means the same in both terminologies.

We have seen how you can do cut/copy/paste operations in Vim. But how do you specify which text that these operations should work on? Well, we have already explored that in the previous [Text Objects section](./moving_around.md#text-objects).

Combining the operation notation and the text object notation means we have innumerable ways of manipulating the text. Let's see a few examples.

Write this text in Vim (exactly as shown):

> This is the rthe first paragraph. <br>
> This is the second line. <br>
> <br>
> This is the second paragraph. <br>

Place the cursor at the topmost leftmost position, by pressing `1G` and `|` that moves to the first line and the first column respectively.

Let's see the first case: We have typed an extra 'r' which we have to remove. Press `3w` to move forward by 3 words.

Now, we need to delete one character at the current cursor position.

Note that there are two parts to this:

| Operation | Text Object / Motion |
| --- | --- |
| Delete | One character at current cursor position |
| `d` | `l` |

So, we have to just press `dl` and we delete one character! Notice that we can use `l` even though it is a motion.

Now we notice that the whole word is redundant because we have "the" twice. Now think carefully on what should be fastest key combination to fix this?

Take some time to think and figure this out for yourself. Take your time. Now read on.

| Operation | Text Object / Motion |
| --- | --- |
| Delete | Word |
| `d` | `w` |

So, press `dw` and you delete a word. Voila! So simple and so beautiful. The beauty is that such simple concepts can be combined to provide such a rich range of possibilities.

How do we achieve the same operation for lines? Well, lines are considered special in Vim because lines are usually how we think about our text. As a shortcut, if you repeat the operation name twice, it will operate on the line. So, dd will delete the current line and yy will yank the current line.

Our example text in Vim should now look like this:

> This is the first paragraph. <br>
> This is the second line. <br>
> <br>
> This is the second paragraph.

Go to the second line by pressing `j`. Now press `dd` and the line should be deleted. You should now see:

> This is the first paragraph. <br>
> <br>
> This is the second paragraph.

Let's see a bigger case: How do we yank the current paragraph?

| Operation | Text Object / Motion |
| --- | --- |
| Yank | A Paragraph |
| `y` | `ap` |

So, `yap` will copy the current paragraph.

Now that we have done copying the text, how do we paste it? Just `p` it.

You should now see:

> This is the first paragraph. <br>
> This is the first paragraph. <br>
> <br>
> <br>
> This is the second paragraph.

Notice that the blank line is also copied when we do yap, so p adds that extra blank line as well.

There are two types of paste that can be done exactly like the two types of inserts we have seen before:

| Key | Mnemonic |
| --- | --- |
| `p` | paste after current cursor position |
| `P` | paste before current cursor position |

Taking the idea further, we can combine these into more powerful ways.

How to swap two characters? Press `xp`.

- `x` &rarr; delete one character at current cursor position
- `p` &rarr; paste after current cursor position

How to swap two words? Press `dwwP`.

- `d` &rarr; delete
- `w` &rarr; one word
- `w` &rarr; move to the next word
- `P` &rarr; paste before the current cursor position

The important thing is *not* to learn these operations by rote. These combinations of operations and text objects/motions should be automatic for your fingers, without you needing to put in mental effort. This happens when you make using these a habit.

## Marking your territory

You are writing, and you suddenly realize you have to change sentences in a previous section to support what you are writing in this section. The problem is that you have to remember where you are right now so that you can come back to it later. Can't Vim remember it for me? This can be achieved using marks.

You can create a mark by pressing m followed by the name of the mark which is a single character from `a-zA-Z`. For example, pressing `ma` creates the mark called 'a'.

Pressing `'a` returns the cursor to line of the mark. Pressing <code>`a</code> will take you to the exact line and column of the mark.

The best part is that you can jump to this position using these marks any time thereafter.

See `:help mark-motions` for more details.

## Time machine using undo/redo

Suppose you are rewriting a paragraph but you end up muddling up what you were trying to rewrite and you want to go back what you had written earlier. This is where we can "undo" what we just did. If we want to change back again to what we have now, we can "redo" the changes that we have made. Note that a change means some change to the text, it does not take into account cursor movements and other things not directly related to the text.

Suppose you have the text:

> I have coined a phrase for myself - 'CUT to the G': <br>
> 1. Concentrate <br>
> 2. Understand <br>
> 3. Think <br>
> 4. Get Things Done <br>
> <br>
> Step 4 is eventually what gets you moving, but Steps 2 and 3 are equally important. As Abraham Lincoln once said "If I had eight hours to chop down a tree, I'd spend six hours sharpening my axe." And to get to this stage, you need to do Step 1 which boils down to one thing - It's all in the mind. That's why it's so hard.

Now, start editing the first line:

1. Press `S` to 's'ubstitute the whole line.
2. Type the text `After much thought, I have coined a new phrase to help me solidify my approach:`.
3. Press `<esc>`.

Now think about the change that we just did. Is the sentence better? Hmm, was the text better before? How do we switch back and forth?

Press `u` to undo the last change and see what we had before. You will now see the text `I have coined a phrase for myself - 'CUT to the G':`. To come back to the latest change, press `ctrl-r` to now see the line `After much thought, I have coined a new
phrase to help me solidify my approach:`.

It is important to note that Vim gives unlimited history of undo/redo changes, but it is usually limited by the `undolevels` setting in Vim and the amount of memory in your computer.

Now, let's see some stuff that really shows off Vim's advanced undo/redo functionality, some thing that other editors will be jealous of: Vim is not only your editor, it also acts as a time machine.

For example, `:earlier 4m` will take you back by 4 minutes i.e. the state of the text 4 minutes "earlier".

The power here is that it is superior to all undoes and redoes. For example, if you make a change, then you undo it, and then continue editing, that change is actually never retrievable using simple u again. But it is possible in Vim using the `:earlier` command.

You can also go forward in time: `:later 45s` which will take you later by 45 seconds.

Or if you want the simpler approach of going back by 5 changes: `:undo 5`.

You can view the undo tree using `:undolist`.

See `:help undolist` for the explanation of the output from this command.

See `:help undo-redo` and `:help usr_32.txt` for more details.

## A powerful search engine but not a dotcom

Vim has a powerful built-in search engine that you can use to find exactly what you are looking for. It takes a little getting used to the power it exposes, so let's get started.

Let's come back to our familiar example:

> I have coined a phrase for myself - 'CUT to the G': <br>
> 1. Concentrate <br>
> 2. Understand <br>
> 3. Think <br>
> 4. Get Things Done <br>
> <br>
> Step 4 is eventually what gets you moving, but Steps 2 and 3 are equally important. As Abraham Lincoln once said "If I had eight hours to chop down a tree, I'd spend six hours sharpening my axe." And to get to this stage, you need to do Step 1 which boils down to one thing - It's all in the mind. That's why it's so hard.

Suppose we want to search for the word "Step". In normal mode, type `/Step<cr>` (i.e. `/Step` followed by `enter` key). This will take you to the first occurrence of those set of characters. Press `n` to take you to the 'n'ext occurrence and `N` to go in the opposite direction i.e. the previous occurrence.

What if you knew only a part of the phrase or don't know the exact spelling? Wouldn't it be helpful if Vim could start searching as and when you type the search phrase? You can enable this by running:

``` viml
set incsearch
```

You can also tell Vim to ignore the case (whether lower or upper case) of the text that you
are searching for:

``` viml
set ignorecase
```

Or you can use:

``` viml
set smartcase
```

When you have `smartcase` on:

- If you are searching for `/step` i.e. the text you enter is in lower case, then it will search for any combination of upper and lower case text. For example, this will match all the following four - "Step", "Stephen", "stepbrother", "misstep."
- If you are searching for `/Step` i.e. the text you enter has an upper case, then it will search for **only** text that matches the exact case. For example, it will match "Step" and "Stephen", but not "stepbrother" or "misstep."

> NOTE: I recommend that you put these two lines in your vimrc file (explained later, but see `:help vimrc-intro` for a quick introduction) so that this is enabled always.

Now that we have understood the basics of searching, let's explore the real power of searching. The first thing to note that what you provide Vim can not only be a simple phrase, it can be a "expression". An expression allows you to specify the 'kinds' of text to search for, not just the exact text to look.

For example, you will notice that /step will take you to steps as well as step and even footstep if such a word is present. What if you wanted to look for the exact word step and not when it is part of any other word? Then you can search using `/\<step\>`. The `\<` and
`\>` indicate the start and end positions of a "word" respectively.

Similarly, what if you wanted to search for any number? Searching for `/\d` will look for a 'digit'. But a number is just a group of digits together. So we specify "one or more" digits together as `/\d\+`. If we were looking for zero or more characters, we can use the `*` instead of the `+`.

There are a variety of such magic stuff we can use in our search patterns. See `:help pattern` for details.

## Summary

We have explored some of the basic editing commands that we will use in our everyday usage of Vim. *It is very important that you go through these concepts again and make them a habit.* It is not important to learn each and every option or nuances of these commands. If you know how to use the command and know how to find out more on it based on what you need, then you're a true Vimmer.

Now, go ahead and start editing!
