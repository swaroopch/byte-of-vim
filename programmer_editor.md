# Programmers Editor

## Introduction

Vim tends to be heavily used by programmers. The features, ease of use, and flexibility that Vim provide make it a good choice for people who write a lot of code. This should not seem surprising since writing code involves a lot of editing.

Let me reiterate that typing skills are critical for a programmer. If our earlier discussion didn't convince you, we hope this article by Jeff Atwood, titled ['We Are Typists First, Programmers Second'](http://www.codinghorror.com/blog/archives/001188.html), will convince you.

If you do not have programming experience, you can skip this chapter.

For those who love programming, let's dive in and see how Vim can help you in writing code. 

## Simple stuff
The simplest feature of Vim that you can use to help you in writing code is syntax highlighting. This allows you to visualize, i.e. "see," your code, which helps you in reading and writing your code faster and helps avoid making obvious mistakes.

### Syntax highlighting
Suppose you are editing a vim syntax file; run `:set filetype=vim` and see how Vim adds color. Similarly, if you are editing a Python file, run `:set filetype=python`.

![Syntax Highlighting for Python](syntax_highlighting.png)

To see the list of language types available, check the `$VIMRUNTIME/syntax/` directory.

#### Tip
    If you want the power of syntax highlighting for any Unix shell output, just pipe it to Vim. For example, `svn diff | vim -R -`.  Notice the dash in the end which tells Vim that it should read text from its standard input.

### Smart indentation
An experienced programmer's code is usually indented properly, which makes the code look "uniform" and the structure of the code more visually apparent. Vim can help by doing the indentation for you so that you can concentrate on the actual code.

If you indent a particular line and want the lines following it to be also indented to the same level, then you can use the `:set autoindent` setting.

If you start a new block of statements and want the next line to be automatically indented to the next level, then you can use the `:set smartindent` setting. Note that the behavior of this setting is dependent on the particular programming language being used.

### Bounce
If the programming language of your choice uses curly brackets to demarcate blocks of statements, place your cursor on one of the curly brackets, and press the `%` key to jump to the corresponding curly bracket. This bounce key allows you to jump between the start and end of a block quickly.

### Shell commands
You can run a shell command from within Vim using the `:!` command.

For example, if the `date` command is available on your operating system, run `:!date` and you should see the current date and time printed out.

This is useful in situations where you want to check something with the file system. For example, you can quickly check which files are in the current directory using `:!ls` or `:!dir` and so on.

If you want access to a full-fledged shell, run `:sh`.

We can use this facility to run external filters for the text being edited. For example, if you have a bunch of lines you want to sort, then you can run `:%!sort`. This passes the current text to the sort command in the shell and then the output of that command replaces the current content of the file.

## Jumping around
There are many ways of jumping around the code.

* Position your cursor on a filename in the code and then press gf to open the file.
* Position your cursor on a variable name and press `gd` to move the local definition of the variable name. `gD` achieves the same for the global declaration by searching from the start of the file.
* Use ]] to move to the next { in the first column. There are many similar motions - see `:help object-motions` for details.
* See `:help 29.3`, `:help 29.4`, and `:help 29.5` for more such commands. For example, `[I` will display all lines that contain they keyword under the cursor!

## Browsing parts of the code
### File system
Use `:Vex` or `:Sex` to browse the file system within Vim and subsequently open the required files.

### ctags
We have seen how to achieve simple movements within the same file, but what if we want to move between different files and have cross-references between files? We can use tags to achieve this.

For simple browsing of the file, we can use the `taglist.vim` plugin.

1. Install the [Exuberant ctags](http://ctags.sourceforge.net) program.
2. Install the [taglist.vim](http://www.vim.org/scripts/script.php?script_id=273) plugin. Refer the "install details" on the script page.
3. Run `:TlistToggle` to open the taglist window. Voila, now you can browse through parts of your program such as macros, typedefs, variables and functions.
4. You can use `:tag foo` to jump to the definition of foo.
5. Position your cursor on any symbol and press `ctrl-]` to jump to the definition of that symbol.
   * Press ctrl-t to return to the previous code you were reading.
6. Use `ctrl-w ]` to jump to the definition of the symbol in a split window.
7. Use `:tnext`, `:tprev`, `:tfirst`, `:tlast` to move between matching tags.

Note that exuberant Ctags supports 33 programming languages as of this writing, and it can easily be extended for other languages.

See `:help taglist-intro` for details.

### cscope
To be able to jump to definitions across files, we need a program like `cscope`. However, as the name suggests, this particular program works only for the C programming language.
1. Install cscope. Refer `:help cscope-info` and `:help cscope-win32` regarding installation.
2. Copy [cscope_maps.vim](http:/\/cscope.sourceforge.net/cscope_maps.vim) to your `~/.vim/plugin/` directory.
3. Switch to your source code directory and run `cscope -R -b` to 'b'uild the database 'r'ecursively for all subdirectories.
4. Restart Vim and open a source code file.
5. Run `:cscope show` to confirm that there is a cscope connection created.
![cscope in action](cscope_in_action.png)
6. Run `:cscope find symbol foo` to locate the symbol `foo`. You can shorten this command to `:cs f s foo`.

You can also:
    * Find this definition - `:cs f g`
    * Find functions called by this function - `:cs f d`
    * Find functions calling this function - `:cs f c`
    * Find this text string - `:cs f t`
    * Find this egrep pattern - `:cs f e`

See `:help cscope-suggestions` for suggested usage of cscope with Vim.

Also, the [Source Code Obedience](http://www.vim.org/scripts/script.php?script_id=1638) plugin is worth checking out as it provides easy shortcut keys on top of cscope/ctags.

While we are on the subject of C programming language, the [c.vim](http://vim.sourceforge.net/scripts/script.php?script_id=213) plugin can be quite handy.

## Compiling
We have already seen in the previous chapter regarding `:make` for the programs we are writing, so we won't repeat it here.

## Easy writing

## Omnicompletion
One of the most-requested features which was added in Vim 7 is "omnicompletion" where the text can be auto-completed based on the current context. For example, if you are using a long variable name and you are using the name repeatedly, you can use a keyboard shortcut to ask Vim to auto-complete and it'll figure out the rest.

Vim accomplishes this via ftplugins, specifically the ones by the name `ftplugin/<language>complete.vim` such as `pythoncomplete.vim`.

Let's start the example with a simple Python program:
```
def hello():
print 'hello world'

def helpme():
print 'help yourself'
```
After typing this program, start a new line in the same file, type 'he' and press `ctrl-x ctrl-o` which will show you suggestions for the autocompletion.

If you get an error like `E764: Option 'omnifunc' is not set`, then run `:runtime!  autoload/pythoncomplete.vim` to load the omnicompletion plugin.

To avoid doing this every time, you can add the following line to your `~/.vimrc:`

![Omni-completion in action](omni_completion_in_action.png)

`autocmd FileType python runtime! autoload/pythoncomplete.vim`

Vim automatically uses the first suggestion, you can change to the next or previous selection using `ctrl-n` and `ctrl-p` respectively.

In case you want to abort using the omnicompletion, simply press `esc`.

Refer `:help new-omni-completion` for details on what languages are supported (C, HTML, JavaScript, PHP, Python, Ruby, SQL, XML, ...) as well as how to create your own omnicompletion scripts.

### Note

    If you are more comfortable in using the arrow keys to select your choice from the omnicompletion list, see [Vim Tip 1228](http://www.vim.org/tips/tip.php?tip_id=1228) on how to enable that.

I prefer to use a simple `ctrl-space` instead of the unwieldy `ctrl-x ctrl-o` key combination. To achieve this, put this in your `vimrc`:

```
imap <c-space> <c-x><c-o>
```
Relatedly, [the PySmell plugin](http://code.google.com/p/pysmell/) may be of help to Vim users who code in Python.

## Using Snippets
Code snippets are small pieces of code that you repetitively tend to write. Like all good lazy programmers, you can use a plugin that helps you to do that. In our case, we use the amazing `SnippetsEmu` plugin.
1. Download the [snippetsEmu](http://www.vim.org/scripts/script.php?script_id=1318) plugin.
2. Create your `~/.vim/after/` directory if it doesn't already exist.
3. Start Vim by providing this plugin name on the command line. For example, start Vim as `gvim snippy_bundles.vba`
4. Run `:source %`. The 'vimball' will now unpack and store the many files in the appropriate directories.
5. Repeat the same process for `snippy_plugin.vba`

Now, let's try using this plugin.
1. Open a new file called, say, `test.py`.
2. Press the keys `d`, `e`, `f` and then `<tab>`.
3. Voila! See, how `snippetsEmu` has created a structure of your function already. You should now see this in your file:

```
def <{fname}>(<{args}>):
    """
    <{}>
    <{args}>"""
    <{pass}>
    <{}>
```
### Note
    In case you see `def<tab>` and nothing else happened, then perhaps the snippets plugin is not loaded. Run `:runtime! ftplugin/python_snippets.vim` and see if that helps.
4. Your cursor is now positioned on the function name i.e. `fname`.
5. Type the function name, say, `test`.
6. Press `<tab>` and the cursor is automatically moved to the arguments. Tab again to move to the next item to be filled.
7. Now enter a comment: `Just say Hi`
8. Tab again and type `print 'Hello World'`
9. Press `<tab>`
10. Your program is complete!
 
You should now see:
```
    def test():
    """
    Just say Hi
    """
    print 'Hello World'
```
The best part is that SnippetsEmu enables a standard convention to be followed and that nobody in the team 'forgets' it.

## Creating Snippets
Let's now see how to create our own snippets.

Let us consider the case where I tend to repeatedly write the following kind of code in ActionScript3:

```
private var _foo:Object;
public function get foo():Object
{
    return _foo;
}
public function set foo(value:Object)
{
    _foo = value;
}
```

This is a simple getter/setter combination using a backing variable. The problem is that's an awful lot of boilerplate code to write repeatedly. Let's see how to automate this.

The SnippetsEmu language snippets plugins assume st `as` the start tag and `et` as the end tag. These are the same arrow-type symbols you see in-between which we enter our code.

Let's start with a simple example.

```
exec "Snippet pubfun public function
".st.et.":".st.et."<CR>{<CR>".st.et."<CR>}<CR>"
```
Add the above line to your `~/.vim/after/ftplugin/actionscript_snippets.vim`.

Now open a new file, say, `test.as` and then type pubfun and press `<tab>` and see it expanded to:

```
public function <{}>:<{}>
{

}

```
The cursor will be positioned for the function name, `tab` to enter the return type of the function, `tab` again to type the body of the function. 

Going back to our original problem, here's what I came up with:

```
exec "Snippet getset private var _".st."name".et.";<CR><CR>public
function get ".st."name".et."():".st."type".et."<CR>{<CR><tab>return
_".st."name".et.";<CR>}<CR><CR>public function set
".st."name".et."(value:".st."type".et.")<CR>{<CR><tab>_".st."name".et."
= value;<CR>}<CR>"
```
### Note
    All snippets for this plugin must be entered on a single line. It is a technical limitation.

Follow the same procedure above to use this new snippet:

1. Add this line to your `~/.vim/after/ftplugin/actionscript_snippets.vim`.
2. Open a new file such as `test.as`.
3. Type `getset` and press `<tab>` and you will see this:

```
private var _<{name}>;

public function get <{name}>():<{type}>
{
       return _<{name}>;
}

public function set <{name}>(value:<{type}>)
{
       _<{name}> = value;
}
```
4. Type `color` and press `<tab>`. Notice that the variable name `color` is replaced everywhere.
5. Type `Number` and press `<tab>`. The code now looks like this:

```
private var _color;

public function get color():Number
{
       return _color;
}

public function set color(value:Number)
{
       _color = value;
}
```
Notice how many keystrokes we have eliminated! We have done away with typing approximately 11 lines of repetitive code with a single Vim script line.

We can keep adding such snippets to make coding lazier and to help us concentrate on the real work in the software.

See `:help snippets_emu.txt` for more details (this help file will be available only after you install the plugin).

## IDE
Vim can be actually used as an IDE with the help of a few plugins.

### Project plugin
The Project plugin is used to create a Project-manager kind of usage to Vim.

1. Download the [project](http://www.vim.org/scripts/script.php?script_id=69) plugin.
2. Unarchive it to your `~/.vim/` directory.
3. Run `:helptags ~/.vim/doc/`.
4. Download Vim source code from [http://www.vim.org/subversion.php](http://www.vim.org/subversion.php)
5. Run `:Project`. A sidebar will open up in the left which will act as your 'project window'.
6. Run `\\c` (backslash followed by 'c')
7. Give answers for the following options:
    * Name of entry, say `'vim7_src'`
    * Directory, say `C:\\repo\\vim7\\src\\`
    * CD option, same as directory above
    * Filter option, say `*.h *.c`
8. You will see the sidebar filled up with the list of files that match the filter in the specified directory.
9. Use the arrow keys or `j/k` keys to move up and down the list of files, and press the enter key to open the file in the main window.

This gives you the familiar IDE-kind of interface, the good thing is that there are no fancy configuration files or crufty path setups in IDEs which usually have issues always. The Project plugin's functionality is simple and straightforward.

You can use the standard fold commands to open and close the projects and their details.

You can also run scripts at the start and end of using a project, this helps you to setup the PATH or set compiler options and so on.

See `:help project.txt` for more details.

## Running code from the text
You can run code directly from Vim using plugins such as [EvalSelection.vim](http://www.vim.org/scripts/script.php?script_id=889) or simpler plugins like [inc-python.vim](http://www.vim.org/scripts/script.php?script_id=1941).

## SCM integration
If you start editing a file, you can even make it automatically checked out from Perforce using the [perforce plugin](http://www.vim.org/scripts/script.php?script_id=240). Similarly, there is a [CVS/SVN/SVK/Git integration plugin](http://www.vim.org/scripts/script.php?script_id=90).

## More
To explore more plugins to implement IDE-like behavior in Vim, see:
* Vim Tip: [Using vim as an IDE all in one](http://vim.wikia.com/wiki/Using_vim_as_an_IDE_all_in_one)
* [C++/Python Vim+IDE plugins list](http://phraktured.net/vimmity-vim-vim.html)
 
There are more language-specific plugins that can help you do nifty things. For example, for Python, the following plugins can be helpful:
* [SuperTab](http://www.vim.org/scripts/script.php?script_id=1643) allows you to call omni-completion by just pressing tab and then use arrow keys to choose the option.
* [python_calltips](http://www.vim.org/scripts/script.php?script_id=1074) shows a window at the bottom which gives you the list of possibilities for completion. The cool thing about this, compared to omni-completion, is that you get to view the documentation for each of the possibilities.
* [VimPdb](http://www.vim.org/scripts/script.php?script_id=2043) helps you to debug Python programs from within Vim.

## Writing your own plugins
You can write your own plugins to extend Vim in any way that you want. For example, here's a task that you can take on:

    Write a Vim plugin that takes the current word and opens a browser with the documentation for that particular word (the word can be a function name or a class name, etc.).

If you really can't think of how to approach this, take a look at "Online documentation for word under cursor" tip at the [Vim Tips wiki](http://vim.wikia.com/wiki/Online_documentation_for_word_under_cursor).

I have extended the same tip and made it more generic:

```
" Add the following lines to your ~/.vimrc to enable online documentation
" Inspiration: http://vim.wikia.com/wiki/Online_documentation_for_word_under_cursor
function Browser()
    if has("win32") || has("win64")
let s:browser = "C:\\Program Files\\Mozilla Firefox\\firefox.exe -new-tab"
    elseif has("win32unix") " Cygwin
let s:browser = "'/cygdrive/c/Program\ Files/Mozilla\ Firefox/firefox.exe' -new-tab"
    elseif has("mac") || has("macunix") || has("unix")
        let s:browser = "firefox -new-tab"
    endif

    return s:browser
endfunction

function Run(command)
    if has("win32") || has("win64")
        let s:startCommand = "!start"
        let s:endCommand = ""
    elseif has("mac") || has("macunix") " TODO Untested on Mac
        let s:startCommand = "!open -a"
        let s:endCommand = ""
    elseif has("unix") || has("win32unix")
        let s:startCommand = "!" let s:endCommand = "&"
    else
        echo "Don't know how to handle this OS!"
        finish
    endif

let s:cmd = "silent " . s:startCommand . " " . a:command . " " .  s:endCommand
    " echo s:cmd
    execute s:cmd
endfunction

function OnlineDoc()
    if &filetype == "viki"
        " Dictionary
let s:urlTemplate = "http://dictionary.reference.com/browse/<name>"
    elseif &filetype == "perl"
let s:urlTemplate = "http://perldoc.perl.org/functions/<name>.html"
    elseif &filetype == "python"
let s:urlTemplate = "http://www.google.com/search?q=<name>&domains=docs.python.org&sitesearch=docs.python.org
    elseif &filetype == "ruby"
let s:urlTemplate = "http://www.ruby-doc.org/core/classes/<name>.html"
    elseif &filetype == "vim"
let s:urlTemplate = "http://vimdoc.sourceforge.net/search.php?search=<name>&docs=help"
    endif

    let s:wordUnderCursor = expand("<cword>")
let s:url = substitute(s:urlTemplate, '<name>', s:wordUnderCursor, 'g')

    call Run(Browser() . " " . s:url)
endfunction

noremap <silent> <M-d> :call OnlineDoc()<CR>
inoremap <silent> <M-d> <Esc>:call OnlineDoc()<CR>a
```
## Access Databases
You can even talk to some 10 different databases from Oracle to MySQL to PostgreSQL to Sybase to SQLite, all from Vim, using the [dbext.vim plugin](http://www.vim.org/scripts/script.php?script_id=356). The best part is that this plugin helps you to edit SQL written within PHP, Perl, Java, etc. and you can even directly execute the SQL even though it is embedded within another programming language and even asking you for values for variables.

## Summary
We have learned how Vim can be used for programming with the help of various plugins and settings. If we need a feature, it can be solved by writing our own Vim plugins (as we have discussed in the Scripting chapter).

A good source of related discussions is at [Stack Overflow](http://stackoverflow.com/questions/tagged/vim) and [Peteris Krumins's blog](http://www.catonmat.net/tag/vim).
