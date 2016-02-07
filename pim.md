## Personal Information Management

A chapter on 'personal information management' (PIM) in a book on an editor software seems strange, doesn't it? Well, there are lots of "professional software" that claim to do personal information management, so let us explore why can't we use a plain text editor like Vim for this purpose?

Personal information management is about organizing all your "information" - such as your todo lists, diary entries, your reference material (such as important phone numbers), scratchpad and so on. Putting all of this in one convenient location can be extremely handy, and we will explore this using Vim and a few plugins.

I tend to think of a PIM system is best organized as a wiki. A wiki is a quick way to link together various documents which are inter-related but are independent in their own right. Unsurprisingly, the word 'wiki' means 'quick' in the Hawaiian language. Think of a website - there is a home page, and there are related pages to which you see links, and each page will have its own content but can also inter-link to other pages. Isn't this an easy way of organizing websites? What if you could do the same for your own personal information? See this [LifeHack article 'Wikify Your Life: How to Organize Everything'](http://www.lifehack.org/articles/lifehack/wikify-your-life-how-to-organize-everything.html) on some great examples on what you can do.

But does this really require a specialized Wiki software? What if you could do the same in just plain text files using Vim? Let's dive in.

## Installing Viki

> NOTE: The `$vimfiles` directory corresponds to `~/.vim` on Linux/Mac, `C:/Documents and Settings/<your-user-name>/vimfiles` on Windows and `C:Users/<your-user-name>/vimfiles` on Windows Vista. See `:help vimfiles` for specific details.

We're going to install Viki and its related plugins:

1. Download [multvals.vim](http://www.vim.org/scripts/script.php?script_id=171) and store as `$vimfiles/plugin/multvals.vim`.
2. Download [genutils.zip](http://www.vim.org/scripts/script.php?script_id=197) and unzip this file to `$vimfiles`.
3. Download [Viki.zip](http://www.vim.org/scripts/script.php?script_id=861) and unzip this file to `$vimfiles` (make sure all the folders and files under the 'Viki' folder name are stored directly in the `$vimfiles` folder)

## Get Started

1. Open the GUI version of Vim
2. `:e test.txt`
3. `:set filetype=viki`
4. Type the following text:

    ```
    [[http://deplate.sourceforge.net/Markup.html][Viki syntax]]
    ```

5. `:w`
6. Position your cursor on the above text and press `ctrl+enter`, or alternatively press `\vf`.
7. You should see a web browser open up with the above website page open.

Similarly, you can write down any file name (with a valid path) - whether it is a `.doc` file or a `.pdf` file and then you can `ctrl+enter` to open the file in the corresponding Word or Acrobat Reader programs!

The idea is that you can use plain text files to *hold* all your thinking together and you can `ctrl+enter` your way into everything else.

Now, notice that we had to type the square brackets in pairs above to identify the target of the link and the words that describe the link. This is basically the syntax of the markup language which we will explore next.

## Markup language

The [Viki syntax](http://deplate.sourceforge.net/Markup.html) page (that you just opened in your web browser) explains how to write the text to allow Viki to syntax highlight portions of your text as well as how to do the linking between 'wiki pages' and even write Viki-specific comments.

Learning the basics of the syntax highlighting is useful because you can visually see the parts of your text file. For example, use `* List of things to do` to make it a header, and then use dashes to create a list:

```
* List of things to do

 - Finish the blog post on Brahmagiri trek
 - Fix footer bug on IONLAB website
 - Buy some blank CDs
 - Get motorbike serviced
```

## Disabling CamelCase

Writing `CamelCase` can create a wiki link in Viki, but I personally dislike this. I prefer that only explicit links like `[[CamelCase]]` be allowed to avoid situations where I have genuinely used a name which uses camel case but I don't want it to be a link (for example, the word "JavaScript"). To disable camel-case syntax, put `let g:vikiNameTypes = "sSeuix"` in your `~/.vimrc` file.

## Getting Things Done

One of the major reasons for creating this 'viki' for myself is to maintain a 'Getting Things Done' system.

[Getting Things Done ("GTD")](http://www.bnet.com/2403-13074_23-52958.html) is a system devised by David Allen to help manage your 'stuff' - which could mean anything from your career plans to the list of chores you have to do today.

From David Allen's book:

> "Get everything out of your head. Make decisions about actions required on stuff when it shows up - not when it blows up. Organize reminders of your projects and the next actions on them in appropriate categories. Keep your system current, complete, and reviewed sufficiently to trust your intuitive choices about what you're doing (and not doing) at any time."

The GTD system basically consists of organizing your information into certain pages/folders:

1. Collection Basket
2. Projects List
3. Next Actions
4. Calendar
5. Someday/Maybe
6. Reference Material
7. Waiting For

I created a viki to match this system by using the following method:

1. First, create a `StartPage` which is literally the start page to your personal organization system (hereby referred to as simply "your viki").
2. Then, create a list of main sections of your viki:

  ```
  * Getting Things Done

  1. [[Collect][In Basket]]
  2. [[Project][Projects List]]
  3. [[NextActions][Next Actions]]
  4. [[Calendar]]
  5. [[SomedayMaybe][Someday/Maybe]]
  6. [[Reference][Reference Material]]
  7. [[Waiting][Waiting For]]
  ```
  
3. Similarly, go to as much depth as you want, for example creating a `[[Reference.Career]]` to jot down your career plans, and `[[Project.TopSecret]]` to gather thoughts on your next project, and so on.
4. Every time you want to jot down something, use the `[[Collect]]` page and then process, organize, review and finally actually do your next-physical-actions.
5. It takes a while to get accustomed to using this system, but once you are comfortable, you can achieve clarity of mind, confidence that you're taking care of all the factors in your life, and most importantly, a sense of direction in knowing what are the important things in your life.

Notice how we are managing an entire system using just plain text!

## Summary

We have just explored how Vim can help you in creating a personal information management system for yourself. It's fascinating how we don't need a complicated software for such a system, just plain text files and Vim will do.

See [Abhijit Nadgouda's article on using Vim as a personal wiki](http://ifacethoughts.net/2008/05/02/vim-as-a-personal-wiki/) for an alternative way of achieving the same using built-in Vim functionality.
