# Scripting

If you want to customize any software, most likely you will change the various settings in the software to suit your taste and needs. What if you wanted to do more than that? For example, to check for conditions such as `if GUI version, then use this colorscheme else use this colorscheme`? This is where "scripting" comes in. Scripting basically means using a language where you can specify conditions and actions put together into 'scripts'.

There are two approaches to scripting in Vim - using the built-in Vim scripting language, or using a full-fledged programming language such as Python or Perl which have access to the Vim internals via modules (provided that Vim has been compiled with these options enabled).

This chapter requires some knowledge of programming. If you have no prior programming experience, you will still be able to understand although it might seem terse. If you wish to learn programming, please refer my other free book [A Byte of Python]({{ book.pythonBookUrl }}).

There are two ways of creating reusable functionality in Vim - using macros and writing scripts.

## Macros

Using macros, we can record sequences of commands and then replay it in different contexts.

For example, suppose you had some text like this:

```
tansen is the singer
daswant is the painter
todarmal is the financial wizard
abul fazl is the historian
birbal is the wazir
```

There are many things to correct here:

1. Change the first letter of the sentence to upper case.
2. Change 'is' to 'was'.
3. Change 'the' to 'a'.
4. End the sentence with "in Akbar's court."

One way would be to use a series of substitute commands, such as `:s/^\\w/\\u\\0/` but this would require 4 substitution commands and it might not be simple if the substitute command changes parts of the text which we do not want to be changed.

A better way would be to use macros.

1. Position your cursor on the first letter of the first line: `tansen is the singer`
2. Type `qa` in normal mode to start recording the macro named as `a`.
3. Type `gUl` to switch the first letter to upper case.
4. Type `w` to move to the next word.
5. Type `cw` to change the word.
6. Type `was`.
7. Press `<Esc>`.
8. Type `w` to move to the next word.
9. Type `cw` to change the word.
10. Type `a`.
11. Press `<Esc>`.
12. Type `A` to insert text at the end of the line.
13. Type `in Akbar's court`.
14. Press `<Esc>`.
15. Type `q` to stop recording the macro.

That looks like a long procedure, but sometimes, this is much easier to do than cook up some complicated substitute commands!

At the end of the procedure, the line should look like this:

```
Tansen was a singer in Akbar's court.
```

Great. Now, let's move on to apply this to the other lines. Just move to the first character of the second line and press `@a`. Voila, the line should change to:

```
Daswant was a painter in Akbar's court.
```

This demonstrates that macros can record complicated operations and can be easily replayed. This helps the user to replay complicated editing in multiple places. This is one type of reusing the manipulations you can do to the text. Next, we will see more formal ways of manipulating the text.

> NOTE: If you want to simply repeat the last action and not a sequence of actions, you do not have to use macros, just press `.` (dot).

## Basics of Scripting

Vim has a built-in scripting language using which you can write your own scripts to take decisions, "do" stuff, and manipulate the text.

### Actions

How do you change the theme i.e. colors used by Vim? Just run:

``` viml
:colorscheme desert
```

Here, I am using the 'desert' color scheme, which happens to be my favorite. You can view the other schemes available by typing `:colorscheme` and then pressing `<tab>` key to cycle through the available schemes.

What if you wanted to know how many characters are in the current line?

``` viml
:echo strlen(getline("."))
```

Notice the names 'strlen' and 'getline'. These are "functions". *Functions* are pieces of scripts already written and have been given a name so that we can use them again and again. For example, the getline function fetches a line and we are indicating which line by the `.` (dot) which means the current line. We are passing the result returned by the `getline` function to the strlen function which counts the number of characters in the text and then we are passing the result returned by the `strlen` function to the `:echo` command which simply displays the result. Notice how the information flows in this command.

The `strlen(getline("."))` is called an expression. We can store the results of such expressions by using variables. Variables do what the name suggests - they are names pointing to values and the value can be anything i.e. it can vary. For example, we can store the length as:

``` viml
:let len = strlen(getline("."))
:echo "We have" len "characters in this line."
```

When you run this line on the second line above in this text, you will get the following output:

``` viml
We have 46 characters in this line.
```

Notice how we can use variables in other 'expressions'. The possibilities of you can achieve with the help of these variables, expressions and commands are endless.

Vim has many types of variables available via prefixes such as `$` for environment variables, `&` for options, and `@` for registers:

``` viml
:echo $HOME
:echo &filetype
:echo @a
```

See `:help function-list` for a huge list of functions available.

You can create your own functions as well:

``` viml
:function CurrentLineLength()
: let len = strlen(getline("."))
: return len
:endfunction
```

Now position your cursor on any line and run the following command:

``` viml
:echo CurrentLineLength()
```

You should see a number printed.

Function names have to start with an upper case. This is to differentiate that built-in functions start with a lower case and user-defined functions start with an upper case.

If you want to simply "call" a function to run but not display the contents, you can use `:call CurrentLineLength()`

## Decisions

Suppose you want to display a different color schemes based on whether Vim is running in the terminal or is running as a GUI i.e. you need the script to take decisions. Then, you can use:

``` viml
:if has("gui_running")
: colorscheme desert
:else
: colorscheme darkblue
:endif
```

How It Works:

- `has()` is a function which is used to determine if a specified feature is supported in Vim installed on the current computer. See `:help feature-list` to see what kind of features are available in Vim.
- The `if` statement checks the given condition. If the condition is satisfied, we take certain actions. "Else", we take the alternative action.
- Note that an `if` statement should have a matching `endif`.
- There is `elseif` also available, if you want to chain together multiple conditions and actions.

The looping statements 'for' and 'while' are also available in Vim:

``` viml
:let i = 0
:while i < 5
: echo i
: let i += 1
:endwhile
```

Output:

```
0
1 
2
3 
4
```

Using Vim's built-in functions, the same can also be written as:

``` viml
:for i in range(5)
:    echo i
:endfor
```

- `range()` is a built-in function used to generate a range of numbers. See `:help range()` for details.
- The `continue` and `break` statements are also available.

## Data Structures

Vim scripting also has support for lists and dictionaries. Using these, you can build up complicated data structures and programs.

``` viml
:let fruits = ['apple', 'mango', 'coconut']

:echo fruits[0]
" apple

:echo len(fruits)
" 3

:call remove(fruits, 0)
:echo fruits
" ['mango', 'coconut']

:call sort(fruits)
:echo fruits
" ['coconut', 'mango']

:for fruit in fruits
: echo "I like" fruit
:endfor
" I like coconut
" I like mango
```

There are many functions available - see 'List manipulation' and 'Dictionary manipulation' sections in `:help function-list`.

## Writing a Vim script

We will now write a Vim script that can be loaded into Vim and then we can call its functionality whenever required. This is different from writing the script inline and running immediately as we have done all along.

Let us tackle a simple problem - how about capitalizing the first letter of each word in a selected range of lines? The use case is simple - When I write headings in a text document, they look better if they are capitalized, but I'm too lazy to do it myself. So, I can write the text in lower case, and then simply call the function to capitalize.

We will start with the basic template script. Save the following script as the file capitalize.vim:

``` viml
" Vim global plugin for capitalizing first letter of each word
"       in the current line.
" Last Change: 2008-11-21 Fri 08:23 AM IST
" Maintainer: www.swaroopch.com/contact/
" License: www.opensource.org/licenses/bsd-license.php

if exists("loaded_capitalize")
  finish
endif
let loaded_capitalize = 1

" TODO : The real functionality goes in here.
```

How It Works:

- The first line of the file should be a comment explaining what the file is about.
- There are 2-3 standard headers mentioned regarding the file such as 'Last Changed:' which explains how old the script is, the 'Maintainer:' info so that users of the script can contact the maintainer of the script regarding any problems or maybe even a note of thanks.
- The 'License:' header is optional, but highly recommended. A Vim script or plugin that you write may be useful for many other people as well, so you can specify a license for the script. Consequently, other people can improve your work and that it will in turn benefit you as well.
- A script may be loaded multiple times. For example, if you open two different files in the same Vim instance and both of them are `.html` files, then Vim opens the HTML syntax highlighting script for both of the files. To avoid running the same script twice and redefining things twice, we use a safeguard by checking for existence of the name 'loaded_capitalize' and closing if the script has been already loaded.

Now, let us proceed to write the actual functionality.

We can define a function to perform the transformation - capitalize the first letter of each word, so we can call the function as `Capitalize()`. Since the function is going to work on a range, we can specify that the function works on a range of lines.

``` viml
" Vim global plugin for capitalizing first letter of each word
"       in the current line
" Last Change: 2008-11-21 Fri 08:23 AM IST
" Maintainer: www.swaroopch.com/contact/
" License: www.opensource.org/licenses/bsd-license.php

" Make sure we run only once
if exists("loaded_capitalize") finish
endif
let loaded_capitalize = 1

" Capitalize the first letter of each word
function Capitalize() range
  for line_number in range(a:firstline, a:lastline)
    let line_content = getline(line_number)
    " Luckily, the Vim manual had the solution already!
    " Refer ":help s%" and see 'Examples' section
    let line_content = substitute(line_content, "\\w\\+", "\\u\\0", "g")
    call setline(line_number, line_content)
  endfor
endfunction
```

How It Works:

- The `a:firstline` and `a:lastline` represent the arguments to the function with correspond to the start and end of the range of lines respectively.
- We use a 'for' loop to process each line (fetched using `getline()`) in the range.
- We use the `substitute()` function to perform a regular expression search-and-replace on the string. Here we are specifying the function to look for words which is indicated by `\\w\\+` which means a word (i.e. a continuous set of characters that are part of words). Once such words are found, they are to be converted using `\\u\\0` - the `\\u` indicates that the first character following this sequence should be converted to upper case. The `\\0` indicates the match found by the `substitute()` function which corresponds to the words. In effect, we are converting the first letter of each word to upper case.
- We call the `setline()` function to replace the line in Vim with the modified string.

To run this command:

1. Open Vim and enter some random text such as 'this is a test'.
2. Run `:source capitalize.vim` - this 'sources' the file as if the commands were run in Vim inline as we have done before.
3. Run `:call Capitalize()`.
4. The line should now read 'This Is A Test'.

Running `:call Capitalize()` every time appears to be tedious, so we can assign a keyboard shortcut using leaders:

``` viml
" Vim global plugin for capitalizing first letter of each word
" in the current line
" Last Change: 2008-11-21 Fri 08:23 AM IST
" Maintainer: www.swaroopch.com/contact/
" License: www.opensource.org/licenses/bsd-license.php

" Make sure we run only once
if exists("loaded_capitalize")
  finish
endif
let loaded_capitalize = 1

" Refer ':help using-<Plug>'
if !hasmapto('<Plug>Capitalize')
  map <unique> <Leader>c <Plug>Capitalize
endif
noremap <unique> <script> <Plug>Capitalize <SID>Capitalize
noremap <SID>Capitalize :call <SID>Capitalize()<CR>

" Capitalize the first letter of each word
function s:Capitalize() range
  for line_number in range(a:firstline, a:lastline)
    let line_content = getline(line_number)
    " Luckily, the Vim manual had the solution already!
    " Refer ":help s%" and see 'Examples' section
    let line_content = substitute(line_content, "\\w\\+", "\\u\\0", "g")
    call setline(line_number, line_content)
  endfor
endfunction
```

- We have changed the name of the function from simply `Capitalize` to `s:Capitalize` - this is to indicate that the function is local to the script that it is defined in, and it shouldn't be available globally because we want to avoid interfering with other scripts.
- We use the `map` command to define a shortcut.
- The `<Leader>` key is usually backslash, `\`.
- We are now mapping `<Leader>c` (i.e. the leader key followed by the 'c' key) to some functionality.
- We are using `<Plug>Capitalize` to indicate the `Capitalize()` function described within a plugin i.e. our own script.
- Every script has an ID, which is indicated by `<SID>`. So, we can map the command `<SID>Capitalize` to a call of the local function `Capitalize()`.

So, now repeat the same steps mentioned previously to test this script, but you can now run `\c` to capitalize the line(s) instead of running `:call Capitalize()`.

This last set of steps may seem complicated, but it just goes to show that there's a wealth of possibilities in creating Vim scripts and they can do complex stuff.

If something does go wrong in your scripting, you can use `v:errmsg` to see the last error message which may give you clues to figure out what went wrong.

Note that you can use `:help` to find help on everything we have discussed above, from `:help \w` to `:help setline()`.

## Using external programming languages

Many people would not like to spend the time in learning Vim's scripting language and may prefer to use a programming language they already know and write plugins for Vim in that language. This is possible because Vim supports writing plugins in Python, Perl, Ruby and many other languages.

In this chapter, we will look at a simple plugin using the Python programming language, but we can easily use any other supported language as well.

As mentioned earlier, if you are interested in learning the Python language, you might be interested in my other free book [A Byte of Python]({{ book.pythonBookUrl }}).

First, we have to test if the support for the Python programming language is present.

``` viml
:echo has("python")
```

If this returns `1`, then we are good to go, otherwise you might want to install Python on your machine and try again.

Suppose you are writing a blog post. A blogger usually wants to get as many people to read his/her blog as possible. One of the ways people find such blog posts is by querying a search engine. So, if you're going to write on a topic (say 'C V Raman', the famous Indian physicist who has won a Nobel Prize for his work on the scattering of light), you might want to use important phrases that helps more people find your blog when they search for this topic. For example, if people are searching for 'c v raman', they might also search for the 'raman effect', so you may want to mention that in your blog post or article.

How do we find such related phrases? It turns out that the solution is quite simple, thanks to Yahoo! Search.

First, let us figure out how to use Python to access the current text, which we will use to generate the related phrases.

``` viml
" Vim plugin for looking up popular search queries related
"       to the current line
" Last Updated: 2008-11-21 Fri 08:36 AM IST
" Maintainer: www.swaroopch.com/contact/
" License: www.opensource.org/licenses/bsd-license.php

" Make sure we run only once
if exists("loaded_related")
  finish
endif
let loaded_related = 1

" Look up Yahoo Search and show results to the user
function Related()
python <<EOF

import vim

print 'Length of the current line is', len(vim.current.line)
EOF
endfunction
```

The main approach to writing plugins in interfaced languages is same as that for the built-in scripting language.

The key difference is that we have to pass on the code that we have written in the Python language to the Python interpreter. This is achieved by using the EOF as shown above - all the text from the `python <<EOF` command to the subsequent `EOF` is passed to the Python interpreter.

You can test this program, by opening Vim again separately and running `:source related.vim`, and then run `:call Related()`. This should display something like `Length of the current line is 54`.

Now, let us get down the actual functionality of the program. Yahoo! Search has something called a [RelatedSuggestion query](http://developer.yahoo.com/search/web/V1/relatedSuggestion.html) which we can access using a web service. This web service can be accessed by using a Python API provided by Yahoo! Search [pYsearch](http://pysearch.sourceforge.net):

``` viml
" Vim plugin for looking up popular search queries related
" to the current line
" Last Updated: 2008-11-21 Fri 08:36 AM IST
" Maintainer: www.swaroopch.com/contact/
" License: www.opensource.org/licenses/bsd-license.php

" Make sure we run only once
if exists("loaded_related")
  finish
endif
let loaded_related = 1

" Look up Yahoo Search and show results to the user
function Related()
python <<EOF

import vim

from yahoo.search.web import RelatedSuggestion

search = RelatedSuggestion(app_id='vimsearch', query=vim.current.line)
results = search.parse_results()

msg = 'Related popular searches are:\n'
i= 1
for result in results:
    msg += '%d. %s\n' % (i, result)
    i += 1
print msg

EOF
endfunction
```

Notice that we use the current line in Vim as the current text we are interested in, you can change this to any text that you want, such as the current word, etc.

We use the `yahoo.search.web.RelatedSuggestion` class to query Yahoo! Search for phrases related to the query that we specify. We get back the results by calling `parse_results()` on the result object. We then loop over the results and display it to the user.

1. Run `:source related.vim`
2. Type the text `c v raman`.
3. Run `:call Related()`
4. The output should look something like this:

```
Related popular searches are:
1. raman effect
2. c v raman india
3. raman research institute
4. chandrasekhara venkata raman
```

## Summary

We have explored scripting using the Vim's own scripting language as well as using external scripting/programming languages. This is important because the functionality of Vim can be extended in infinite ways.

See `:help eval`, `:help python-commands`, `:help perl-using` and `:help ruby-commands` for details.

To dive deep into this topic, see [Learn VimScript The Hard Way by Steve Losh](http://learnvimscriptthehardway.stevelosh.com).
