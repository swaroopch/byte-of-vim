# Help

Vim has such a diverse list of commands, keyboard shortcuts, buffers, and so on. It's impossible to remember how all of them work. In fact, it is not even useful to know all of them. The best situation is that you know how to look for certain functionality in Vim whenever you need it.

For example, you want to avoid having to type a long name every time, you suddenly remember there is an abbreviations feature in Vim that'll help you do just that, but don't remember how to use it. What do you do?

Let's look at the various ways of finding help about how to use Vim.

## The `:help` command

The first and most important place to try to look for help is the built-in documentation and Vim has one of the most comprehensive user manuals that I've ever seen.

In our case, just run `:help abbreviation` and you'll be taken to the help for abbreviations and you can read about how to use the `:ab` and `:iab` commands.

Sometimes, it can be as simple as that. If you don't know what you're looking for, then you can run `:help user-manual` and browse through the list of contents of the entire user manual and read the chapter that you feel is relevant to what you're trying to do.

## How to read the `:help` topic

Let us take some sample text from `:help abbreviate`:

```
    :ab[breviate] [<expr>] {lhs} {rhs}
                add abbreviation for {lhs} to {rhs}.  If {lhs} already
                existed it is replaced with the new {rhs}.  {rhs} may
                contain spaces.
See |:map-<expr>| for the optional <expr> argument.
```

Notice that there is a standard way of writing help in Vim to make it easy for us to figure out the parts that are needed for us instead of trying to understand the whole command.

The first line explains the syntax i.e. how to use this command.

The square brackets in `:ab[breviate]` indicate that the latter part of the full name is optional. The minimum you have to type is `:ab` so that Vim recognizes the command. You can also use `:abb` or `:abbr` or `:abbre` and so on till the full name `:abbreviate`. Most people tend to use the shortest form possible.

The square brackets in `[<expr>]` again indicate that the 'expression' is optional.

The curly brackets in `{lhs} {rhs}` indicate that these are placeholders for actual arguments to be supplied. The names are short for 'left hand side' and 'right hand side' respectively.

Following the first line is an indented paragraph that briefly explains what this command does.

Notice the second paragraph which points you to further information. You can position the cursor on the text between the two pipe symbols and press `ctrl-]` to follow the "link" to the corresponding `:help` topic. To jump back, press `ctrl-o`.

## The `:helpgrep` command

If you do not know what the name of the topic is, then you can search the entire documentation for a phrase by using `:helpgrep`. Suppose you want to know how to look for the beginning of a word, then just run `:helpgrep beginning of a word`.

You can use `:cnext` and `:cprev` to move to the next and previous part of the documentation where that phrase occurs. Use `:clist` to see the whole list of all the occurrences of the phrase.

## Quick help

Copy the following text into a file in Vim and then also run it:

``` viml
:let &keywordprg=':help'
```

Now, position your cursor anywhere on the word `keywordprg` and just press `K`. You'll be taken to the help immediately for that word. This shortcut avoids having to type `:help keywordprg`.

## Mailing List

If you are still not able to figure out what you want to do, then the next best thing is to approach other Vim users to help you out. Don't worry, this is actually very easy and it is amazing how other Vimmers who are willing to help you out.

Search the Vim mailing list to see if someone has already answered your question. Just go to the [Vim Group search page](http://groups.google.com/group/vim_use) and then enter the keywords of your question. Most of the times, many common questions will be already answered since this is such a high-traffic mailing list i.e. lots and lots of people ask questions and give answers in this group.

If you cannot find any relevant answer, then post your question in the same mailing list.

## Summary

There is a wealth of information on how to do things using Vim, and many Vimmers would gladly help you out as well. The Vim community is one of the greatest strengths of the Vim editor, so make sure to use the resources and do join the growing community as well.

> The true delight is in the *finding out* rather than in the *knowing*.
> -- Isaac Asimov
