
To Henry,
========

# Merry Christmas!

Wow, what a year it's been. I hope you're doing okay. I thought I would make
you something this year in the same spirit you'll be making all of us
something.

I know you wanted to get into programming so I thought I would write up a few
bits of information on where to start and some of the most useful resources
I've used. I think you mentioned you wanted to learn a bit of Node.js and that
you had a Raspberry pi so I've written this guide with that in mind.

# The basics

I'll start with the very basics that will be useful to you whatever you're
wanting to program.

## terminals + shells

Terminals are a fascinating bit of legacy software that have survived for, well
legacy reasons. In the past, personal computers used to boot into a full-screen
terminal, and for that reason personal computers were actually referred to _as_
terminals. Nowadays terminals are programs that run essentially the same
software but render the final output to a GUI, which is typically a window-based
system.

On macOS for example, you'll find Terminal.app that implements a terminal
wrapped in a Cocoa GUI.

A terminal (not shell) is a program that is responsible for outputting text to a
screen. Most of the time you will not have to care about what terminals are or
what they do. This is generally because the only program you will ever run
inside a terminal is a _shell_.

A shell is a program that provides an interactive interface for running
commands. There are a few different shells out there but the most commonly used
is `bash`.

### `bash`

When you open e.g. Terminal.app on macOS, it will automatically start `bash` in
every tab you open. `bash` allows you to run commands, which will come in handy
when you're testing code, running programs, deploying code, basically anything
related to software development. Most guides out there will start with the
assumption that you can run commands in a shell so I can recommend getting
comfortable with it.

On Windows, you can run `bash` if you've installed
[WSL](https://docs.microsoft.com/en-us/windows/wsl/) (I think).

Apart from running commands, `bash` is useful for executing multiple commands in
a sequence from a file called a script. It has loops, variables, conditionals,
functions and can call any command.

Here's a script I wrote:

```bash
# merry_christmas.sh

# Loop over all foreground/background colours, print
for i in {1..255}; do
  printf "\e[38;5;$i""m Merry\e[m \e[48;5;$i""m\e[37mChristmas\e[m"
  if [[ $((i%=8)) -eq 0 ]];
    then printf "\n";
  fi
done
```

Try pasting the above into a file and running it:
```bash
 $ bash merry_christmas.sh
```

The output you should have seen should look a bit like this:

![](./screenshot_1.png)

I won't go into the details about how terminals and shells interact because you
generally don't need to know. There's a
[section on it at the end](https://github.com/lukebarnard1/christmas#what-do-terminals-actually-do)
if you really want to know wtf is going on there.

### Links
  - [introduction to bash by Microsoft](https://docs.microsoft.com/en-us/learn/modules/bash-introduction/) - this includes some of the basics of using a few basic commands
  - [bash cheat sheet](https://devhints.io/bash) - useful for quick reference of different syntax

## editors

Editing files is something you'll do a lot if you're writing code all the time,
which makes it all the more important to choose an editor that suits you best.

Most devs I know have opted for [VSCode](https://code.visualstudio.com/), which
is a free, super-powerful IDE with many many extensions that will probably give
you everything you would ever need in your coding life, including integration
with `git`.

Some prefer to press fewer keys and avoid using a mouse/trackpad at _all_ costs, in
which case I can highly recommend checking out the terminal-based editor, _vim_.
The controls in vim are very different to your average editor, namely due to the
fact that you move the cursor with the keys "hjkl". To insert text, you press
"i" and then type what you want to insert, followed by the escape key. Let's
just say it takes a while to get used to (and eventually you find yourself typing
"jhkhljhkl" into every text field...)

Anyway, if you want to sip the vim cool-aid, I can recommend getting a license for [Vim
adventures](https://vim-adventures.com/) which is surprisingly fun and basically
the only effective way to learn how to control vim. My preferred implementation
of vim is
[Neovim](https://github.com/neovim/neovim/wiki/Installing-Neovim#install-from-download)
if you're really interested in having a go.

Also, you will find the precursor to `vim` - _vi_ - installed in most places by
default, so it can come in handy to know the basics. On the other hand, `nano`
is also installed in most places and has controls that are similar to most IDEs
but having learned how to use `vim` I can confirm that `nano` is actually trash.

I will say, using `vim` does come with a lot of caveats, the main one being that
you have to do more work to get it set up in a way that even comes close to what
editors like VSCode can do out of the box.

## git

Git allows programmers to track changes to the files they're working on. These
files could be source code files, images, READMEs (like this) or literally any
kind of file. Git generally works better with files that are text-based because
it's optimised to track changes in large code bases with millions of lines of
code.

Apart from file version tracking, git is also built to distribute a repository of code
between multiple developers. This means that there isn't really a distinction
between the repo on the git "server" vs. the repo on the git "client". One copy
of a git repo is all you need to preserve it, which is one of the many reasons
it's so popular.

[GitHub.com](https://github.com) is the most popular git repo hosting service
out there as often confused with git itself, but they're not equivalent. For
example, I run my own git server for deploying my personal website and there are
only two copies: one on my laptop and one on my server. I _could_ upload it to
GitHub but I don't really have a need and it's quite nice to keep all of that
code private!

Fun fact, git was originally built to track changes to the source code of linux
so you know it's legit.

To learn about git, I can highly recommend the Pro Git book, which has some
great introductory sections on how git works [available for free, here](https://git-scm.com/book/en/v2).
It's not essential to know how it works but it does help a hell of a lot when
you're trying to use it. Having a decent mental model of git should save you a
lot of time in the long run, even for smaller projects. The first three chapters
should generally be enough for most things you will ever do with git.

Something you might want to try out is cloning this repository and running
and/or messing with the scripts I've put here, e.g.
[merry_christmas.sh](./merry_christmas.sh):

```bash
 $ git clone https://github.com/lukebarnard1/christmas
 $ cd christmas
 $ sh merry_christmas.sh
```

## `man`

This command is particularly useful when you have no idea how a certain command
works. Running `man [command]` will give you an interactive view of the "man
file" for that command.

For example, run `man ls` to see how the `ls` command functions, or `man node`
for documentation of the `node` program.

When `man` is open, the controls are a bit different to what you may be used to.
For example, scrolling might not work but the arrow keys do. This is because
`man` is using another program under the hood to "page" through the content it's
displaying. The `less` command provides the same interface. Here are some of the
controls:

 - 'q': quit
 - 'j/k': scroll down/up
 - 'g': scroll to the top
 - 'G': scroll to the bottom
 - '/[query]': search forwards for the text _[query]_
 - '?[query]': search backwards for the text _[query]_
 - '&[query]': only display lines with text _[query]_

## cheat sheets

Once you've got the basics down, cheat sheets are great for quick reference. I'm
not ashamed to admit I still use the `bash` one _a lot_.

 - `bash`: https://devhints.io/bash
 - `git`: https://about.gitlab.com/images/press/git-cheat-sheet.pdf

# Node.js

Node.js is fantastic for a number of different use cases, namely running a web
server with very little overhead. Most tutorials for Node.js will start with
exactly this use-case for that reason so I won't duplicate them here.

Note that Node.js is a runtime built on Google's [V8 engine](https://v8.dev/).
And V8 is the thing that actually interprets the code that you run, that is to
say it implements that language. In this case, the language is commonly known as
_JavaScript_ but has the official name of
[_ECMAScript_](https://tc39.es/ecma262/) (which was never going to catch on, but
it's a standard so they can't exactly go back and change it).

This is a complicated way of saying that Node.js uses V8 to _interpret_ the JS
but has the primary purpose of exposing the host system through a set of
APIs. These APIs provide control over the file system, network and standard
input/output, as well as providing a set of standard modules for common tasks
such as:
 - [Buffer](https://nodejs.org/dist/latest-v15.x/docs/api/buffer.html)
   for the encoding and manipulation of text or binary data
 - [Crypto](https://nodejs.org/dist/latest-v15.x/docs/api/crypto.html)
   for encryption, decryption, generating key pairs etc.
 - [Process](https://nodejs.org/dist/latest-v15.x/docs/api/process.html)
   for control over the current Node.js process
 - [Readline](https://nodejs.org/dist/latest-v15.x/docs/api/readline.html)
   for reading input from the parent process (standard input)

I wouldn't ever say you could "learn" Node.js as much as you can memorise all of
its many many APIs. Personally, I tend to figure out exactly what I need for a
given project, implement it, maybe leave some comments about how it works and
then quickly proceed to forget everything I needed to know about that particular
Node.js API.

## Links
 - [introduction to node](https://nodejs.dev/learn) - a comprehensive guide to
   getting started with Node.js. I've actually never read this but it looks
   great from a quick skim.
 - [Node.js documentation](https://nodejs.org/en/docs/) - the official docs for
   Node.js. This will come in handy when you need to know how a certain node.js
   API works.
 - [w3schools Node.js and Raspberry Pi
   tutorial](https://www.w3schools.com/nodejs/nodejs_raspberrypi.asp) - this
   looks like a fun tutorial to get Node.js running on Raspberry Pi, including a
   few example projects involving LEDs(!)
 - [express.js](https://expressjs.com/en/starter/hello-world.html) - express.js
   is your go-to for getting a Node.js-based web server up and running. This
   could be the backend for a web app that needs access to a database for
   example.

## JavaScript

JavaScript -- or _ECMAScript_, as it's officially known -- was written in one
week by a developer working on one of the first web browsers, Netscape. As such
it's a [bit](https://charlieharvey.org.uk/page/javascript_the_weird_parts) [weird (skip to 1:23)](https://www.destroyallsoftware.com/talks/wat).



### Links
 - [codecademy - introduction to javascript](https://www.codecademy.com/learn/introduction-to-javascript) - a web-based tutorial on JavaScript for beginners.
 - [you don't know js yet](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/get-started/ch1.md) - an incredibly thorough deep-dive on everything JavaScript. I would recommend having a few months experience before reading this from start-to-finish. However, it does have some useful chapters on concepts like [scope and closures](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures) and [`this`](https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/this%20%26%20object%20prototypes/ch1.md) which is _suprisingly_ subtle.


## TypeScript

You might be interested in learning about TypeScript, so I've mentioned it here
for completeness. I have only just started properly learning about TypeScript
myself.

Essentially TypeScript allows you to check that for a given JavaScript program,
the types of values that move through the program are always valid. It is a
superset of JavaScript so any JavaScript program can be interpreted as
TypeScript without any type annotations.

These type annotations are how the programmer indicates the values that are
expected in certain variables.

It stops you from running JavaScript that you probably didn't intend such as
this perfectly valid JavaScript:

```js
console.info([ ] + { }) // prints '[object Object]', obviously
```

The above example is contrived -- TypeErrors are a real problem in real
production systems and TypeScript prevents them completely. One way it does this
is by tracking the types of certain expressions through the code such
that you can never call the `+` operator in the way I mentioned above, for
example.

### Links
 - [introduction to TypeScript for the new programmer](https://www.typescriptlang.org/docs/handbook/typescript-from-scratch.html) - this looks to be a really good starting point for newbie TypeScript programmers with little experience in programming.

## advanced stuff

### what do terminals actually do?

Terminals today are programs that interpret the output of other programs in
order to render a text-based interface to a screen.

To illustrate how exactly this works, I'll use the example of the text "man
bash" being entered into the terminal, followed by the <kbd>enter</kbd> key.

Let's start with pressing the "m" key:
  1. The key m is pressed
  2. The keyboard driver software handles a signal the indicates that the "m"
     key has been pressed
  3. The terminal GUI program runs some code that handles this signal, passing
     the character "m" as data to the program currently running, which in this
     case is `bash`.
  4. `bash` receives this data and does the following:
     a. prints the character "m" at the current cursor position (output: "m")
     b. moves the cursor position one place to the right (output: "\e[C")
  5. The terminal receives the character "m" and the control sequence, updating
     the visible buffer accordingly after each one.

The important steps are 4 & 5. In step 4, the terminal sends data to `bash` and
`bash` responds by sending some output immediately. The output in 4.a indicates
to the terminal that the character "m" should be printed at the current cursor
location. The output in 4.b indicates to the terminal that the cursor position
should move one position to the right. The terminal distinguishes the sequence
from text output thanks to the "\e\[" sequence. This sequence of bytes (which is
often denoted "ESC \[" and can be output with the `printf` command with the
string "\e\[" or "\033\[") is known as the _Control Sequence Introducer_. This
sequence indicates to the terminal that the next few characters are likely part
of a _Control Sequence_.

The cool thing is that you can output these sequences from your own programs
(well I think it's cool anyway). So if you ever want your program to run in a
terminal and have blinking green text, you can do that! For details on every
single code that was ever probably implemented, see
[this mad bit of documentation from the fringes of the web](https://invisible-island.net/xterm/ctlseqs/ctlseqs.html)

### help! my shell prompt is boring 😱

By far the most common use of control sequences for programmers just starting
out is customising the "prompt" in your shell, which is the text that is printed
before you enter a command. There are even [tools on the web](http://bashrcgenerator.com/)
to simplify the process of picking your favourite colours 😍.

For example, you might want to go for a bright pink with white text and a star
emoji:

```
 $ export PS1='\e[48;5;200m\e[38;5;255m\w ⭐️ $ '
```

, which just FYI looks bad-_ass_:

![](screenshot_2.png)

Looking at that command above, you'll notice the word `export` - this is for
setting environment variables in the current shell session. You can inspect the
values of environment variables by running `echo $NAME`, so for example if you
wanted to check the value assigned to `PS1`, you could run `echo $PS1`.
`




