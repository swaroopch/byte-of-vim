# Introduction

## What is Vim?

Vim is a computer program used for writing any kind of text, whether it is your shopping list, a book, or software code.

What makes Vim special is that it is one of those few software which is both **simple and powerful**.

Simple means it is easy to get started with. Simple means that it has a minimalistic interface that helps you to concentrate on your main task - writing. Simple means it is built around few core concepts that helps you learn deeper functionality easily.

Powerful means getting things done faster, better and easier. Powerful means making not-so-simple things possible. Powerful does not mean it has to be complicated. Powerful means following the paradigm of **"Minimal effort. Maximal effect."**

## What can Vim do?

I can hear you say, "So it's a text editor. What's the big deal anyway?"

Well, a lot.

Let's see some random examples to compare Vim with your current choice of editor. The point of this exercise is for you to answer the question *"How would I do this in the editor I currently use?"* for each example.

> NOTE: Don't worry too much about the details of the Vim commands here, the point here is to enlighten you with the possibilities, not to start explaining how these things work. That is what the rest of the book is for.

| Edit | In Vim | In your editor |
| ---- | ------ | -------------- |
| How do you move the cursor down by 7 lines? | Press `7j` | (Fill this column) |
| How do you delete a word? Yes, a "word" | Press `dw` | |
| How do you search the current file for the current word that the cursor is at? | Press `*` | |
| How to find and replace only in lines 50-100? | Run `:50,10s/old/new/g` | |
| How to view two different parts of the same file simultaneously? | Run `:sp` to 'split' the view | |
| The cursor is at a file name, how to jump to that file? | Press `gf` (which means 'g'o to 'f'ile) | |
| Switch to a better theme? | Run `:colorscheme desert` to choose the `desert` theme | |
| How to map `ctrl-s` to save the file? | Run `:nmap <c-s> :w<CR>` (`<CR>` means 'c'arriage 'r'eturn, i.e. the enter key) | |
| How to save the current set of open files & settings so that you can restart the session later? | Run `:mksession ~/session.vim` and then open Vim next time with `vim -S ~/session.vim` | |
| How to see colors for different parts of your code? | Run `:syntax on`. If it doesn't recognize the language properly, use `set ft=python` for example. | |
| How to hide different parts of the file so that you can concentrate on only one part at a time? | Run `:set foldmethod=indent` assuming your file is properly indented. | |
| How to open multiple files in tabs? | Use `:tabedit <file>` to open multiple files in "tabs" (just like browser tabs), and use `gt` to switch between tabs | |
| You use some words frequently in your document and wish there was a way that it could be quickly filled in the next time you use the same word? | Press `ctrl-n` to see the list of "completions" for the current word, based on all the words that you have used in the current document. Alternatively, use `:ab mas Maslow's hierarchy of needs` to expadn the abbreviation automatically when you type `m a s <space>`. | |
| You have some data where only the first 10 characters in each line are useful and the rest is no longer useful for you. How do you get only that data? | Press `ctrl-v`, select the text and press `y` to copy the selected rows and columns of text. | |
| What if you received a document from soneone which is all in cas, find it irritating and want to convert it to lower case? | (1) Run the following: `:for i in range(0, line('$')) | call setline(i, tolower(getline(i))) | endfor`. <br> (2) Don't worry, details will be explored in later chapters. A more succinct way would be to run `:%s#\\(.\\)#\\l\\1#g`, but the first way would be simpler. (3) Select all the text using `1GVG` and then using the `u` operator to convert the selection to lowercase. | |

Phew. Are you convinced yet?

In these examples, you can see the power of Vim in action. Any other editor would make it insanely hard to achieve the same level of functionality. And yet, amazingly, all this power is made as understandable as possible.

Notice that we didn't use the mouse even once during these examples! This is a good thing. Count how many times you shift your hand between the keyboard and the mouse in a single day, and you'll realize why it is good to avoid it when possible.

Don't be overwhelmed by the features here. The best part of Vim is that you don't need to know all of these features to be productive with it, you just need to know a few basic concepts. After learning those basic concepts, all the other features can be easily learned when you need them.
