# The CLI (Command Line Interface)

## Learning Objectives

- Define and explain the strengths and weaknesses of GUIs and CLIs
- Learn how to access the terminal and break down its components
- Describe the file system and how it relates to the CLI
- Introduce common commands and list unsafe ones
- Learn how to find more information on using commands
- Introduce Bash and how to customize the command line

## Framing (10 minutes / 0:10)

The majority of our interactions with computers so far have been through the graphical user interface (GUI) - the visual and spatial representation of the filesystem on our computer. The GUI is a great tool, it's what made modern consumer computing possible.

While the GUI is perfect for the average computer user, there are drawbacks for power users:

- GUIs are slow - we can only work as fast as we can move and click with our mouse
- GUIs are inflexible - we can only perform tasks in an application that the application creators preconceived
- GUIs require manual effort - anything we want to achieve through a GUI we have to do by pointing and clicking ourselves

As a budding web developer, you are on your way to becoming a computer power user and will soon start to feel these limitations (if you haven't already). This is where the Command Line comes in.

The Command Line is a text-based interface for navigating and working with the file system on your computer. "Text-based" means you interact with it with text commands that are interpreted. There are a lot of different commands you can learn, each of which only performs a single action. You can use these commands as they are for performing simple tasks or you can combine them to perform really complex tasks.

#### Turn & Talk (10 minutes / 0:20)
Given your exposure to the Command Line in the pre-work and Installfest, spend **5 minutes** discussing and writing down a few answers for the following questions with a partner.

* How is the CLI different from the GUI?
* What do you like / dislike about using it?
* Compared to a GUI, in what ways might using the CLI be better or worse for developers?

### Benefits of the CLI (10 minutes / 0:30)

**Power/Speed.** Many tasks can be accomplished much faster using the CLI. Features such as tab completion,
command history, piping (sending the output of one command to another for additional processing) and more all contribute to this.

**Precision.** We can look at the commands we're about to enter and understand exactly what they will do.

**Repeatability / Scriptability.** We can easily save commands and re-use them, or even share them with others.

What you did during Installfest was run a script that we shared with you!

**Tools.** There are tons of tools (programs really) we can run from the CLI. Most of them are built in, but we can also download external ones using services like Homebrew (OSX) and `apt-get` (Linux).

Tools built for the command line usually follow something called the ['Unix philosophy'](http://catb.org/esr/writings/taoup/html/#id2807216), meaning each tool should do one thing and do it well. Complex tasks can be achieved by chaining tools together.

**Debugging.** Whenever we get an error in the CLI, it will often come with a lot of information that we can use to then debug it. As developers, this is preferable to what can often be unhelpful GUI errors.

![unhelpful error](./assets/unhelpful-error.png)

## CLI Basics (15 minutes / 0:45)

### The Terminal and the Shell

How do we get at this text-based interface from our GUI desktop? We run what's called a terminal application (also often referred to as a terminal emulator). The default on OSX is `Terminal.app`. When you open a new Terminal window, the Terminal app will call a program called a **shell**.

A shell is a program that takes commands, passes them to the operating system and returns any output or errors. The default shell used by terminal is called **Bash**. There are other shells but all operate very similarly.

Let's fire up our terminals and get exploring!

### Getting Oriented

First, open Terminal by clicking the icon on your dock, finding the application in Applications > Utilities > Terminal, or using Spotlight (**&#x2318; + SPC**)

You should see something like the following prompt:

![Command Line Prompt](./assets/cl_prompt.png)

The prompt is the shell asking for input; when you see `$ <something>` in documentation, it generally means, input this command into a shell.

If you have a terminal open but do not see a prompt, that means that the shell is not ready to receive input.

Typing a random string of characters and hitting enter will produce a message `-bash: <your-random-string>: command not found`
![Command not found](./assets/command_not_found.png)

> What is a command?

A command is a program. Some come built into the shell and provide the basics for interacting with the operating system and some are written by programmers (like you!) to provide further functionality.

## Break (10 minutes / 0:55

## File System (45 minutes / 1:40)

In the next section of this lesson, we're going to work through a couple of commands that you'll end up using almost every day as a developer. The commands can be divided into two kinds of tasks: Navigating around the file system and working with files and directories. 

### Navigating the File System

The first set of commands we'll cover are for navigating: getting form one directory to another.

You may have seen these commands before (maybe in the prework):

| command | definition |
| --- | --- |
| `pwd` | print working directory |
| `ls` | list files and directories |
| `cd` | change directory |

How do these relate to navigating? 

If we're inside the terminal and we want to travel through our file system to a specific directory (i.e. `traverse`), we first need to know where we are. That's what we use `pwd` for: printing the directory we're in currently.

Once we know where we are, it makes sense to figure out where we can go from here. We use `ls` for that: listing all the files we can work with directly and the directories we can move to.

To move from our current directory to another directory, we use the `cd` command. `cd` moves us from our current directory to another directory that we supply a path to.

You can think of a path as being similar to an address. There are two types of paths: *absolute* and *relative*.

A *relative* path is similar to giving someone directions to a destination from their current location. Where is General Assembly? Two blocks up 15th street from where you are now.

An *absolute* path is similar to giving someone coordinates to a  destination. Where is General Assembly? 38.9048728, -77.0340283.  An important aspect of an *absolute* path is the starting point. In a coordinate system (like longitude and latitude) that is the coordinates 0, 0 (where the equator crosses the prime meridian). In our file system it's the *root* directory, symbolized as `/`.

Here is how that translates into actual commands you could run to navigate to your `Documents/` directory:

**Relative Path:**
```sh
cd ./Documents/
```

**Absolute Path:**
```sh
cd /Users/wdistudent/Documents
```

In the *relative* path, the leading `./` stands for: *from the current directory*. In the *absolute* path, the leading `/Users/wdistudent/` means from the root of the file system, the `Users/` directory and then the `wdistudent/` directory. The `wdistudent` directory has a special name too: the *home* directory.

#### Go Explore

Using the commands you've learned, go explore your file system for a few minutes. When you open a new terminal window and run `ls`, where in the file system are you? What do you see? Compare that to opening a new window in `Finder`.

#### [You Do: Directory Tree](https://ga-wdi-exercises.github.io/dc_directory_tree/) (15 minutes / 1:55)

### Working with Files and Directories

Now that we can navigate the file system, it's time to chart our own paths (pun intended).

The commands we'll be covering next are:

| Command | Description |
| --- | --- |
| `mkdir` | make a new directory |
| `rmdir` | remove a directory |
| `touch` | create a new file |
| `rm` | remove a file |
| `mv` | move a file or directory |
| `cp` | copy a file or directory |

#### WDI Environment (5 minutes)

To get your hands dirty, use the commands above to build out the following folders and files. This will be where you store all your work from WDI.

```sh
wdi
  ├── homework
  ├── labs
  ├── lessons
  │   └── cli_intro.md
  ├── projects
  └── sandbox
```

**Pro Tip:**
Use brackets to substitute paths together. Lets say you want to create a markdown file (extension `.md`) for a couple of lessons. One way to do this would be to run the commands one-by-one:

```sh
touch lessons/cli_intro.md
touch lessons/git_intro.md
touch lessons/html.md
touch lessons/css.md
```

That would absolutely work, but you could make do it in one command:

```sh
touch lessons/cli_intro.md lessons/git_intro.md lessons/html.md lessons/css.md
```

That would also work, but we can make it a more succinct command by using substitution:

```sh
touch lessons/{cli_intro,git_intro,html,css}.md
```

The above command will create the same set of files, but in one short command. It also works with directories! The list of file or directories must be separated by commas with *no spaces*.

### Output and Side Effects

Some commands have **output**, which is displayed on the screen for us to see. Examples of commands that have output are...

* `pwd`
* `ls`
* `brew install tree`.

Other commands' primary purpose is to execute some **side-effect**, or in other words, to make some change that isn't necessarily printed in the Terminal after hitting enter.

Often times, a command whose main job is a side effect may not provide any output if it succeeds. If there is an error, it will provide output (we would get an error if there were a problem so no news is good news).

> What's an example of this we've already seen?

Another example would be `touch`. This command creates a file in an indicated location. We do not, however, get a confirmation it did this immediately after hitting enter.

> Related to touch, what do you think `mkdir` does?

Some commands may provide both an output and side effects.

### Command Syntax

Commands generally consist of three parts

1. Command
2. Options
3. Arguments

The **Command** is the first word you type into the CLI (e.g. `ls`, `cd`, or `touch`). Think of it as the "verb" which indicates what we want to do.

Next come the **Options**, sometimes called flags or switches.
* Sometimes you won't be using any options. Other times you may use several
* By convention, options will start with a dash or two; one if the option is a single letter and two for the "long" name
* Sometimes an option takes an argument. In these cases, the argument comes right after the option

Finally come the **Arguments**. These are "targets", or what you want to do the action to. These could be file names, URLs, etc.

### Common Patterns

The commands entered into the CLI are often in one of the following forms..

- `doSomething --how toFiles`
- `doSomething --how sourceFile destinationFile`

Where **doSomething** is, in effect, a verb, **how** an adverb (for example, should the command be executed "verbosely" or "quietly") and **toFiles** an object or objects (typically one or more files) on which the command should act.

Not all commands follow this pattern, but many do.

Let's take a look at something we did for installfest.

```
$ brew install tree
```

When we type this command and hit enter, we're saying, "Computer, we're about to do something with homebrew. The thing were going to do is install something. What we want to install is `tree`.

> Spend 2 minutes writing down the commands, options, and arguments for each of the below commands. (some may not have flags and/or arguments.)
  1. `$ touch index.html`
  2. `$ ls -al`
  3. `$ cp index.html index2.html`
  4. `$ brew install git`
  5. `$ mkdir -p lessons/sandbox`

## Getting Help

There are three general ways to get help with a command.

* Add `--help` or `-h` to the end of the command (e.g., `brew --help`).
* Use the manual - or `man` - tool (e.g., `man brew`).
* Google!

The `man` will display the man pages using a program `less`. Use the arrow keys to navigate. Type `q` to quit. Use `/` to search and `n` and `p` to go to the next or previous search result

## Break (10 minutes)

## Common Command Teachbacks (25 minutes)

> 15 minutes preparation. 10 minutes review.

Form groups of 3 and spend 10 minutes researching and preparing a short demo of your command. Focus on...

* What it does.
* Common uses.
* Common flags or arguments.
* Any "gotchas" (i.e., things we should be aware of when using this command)?

**Tip:** use the `man` pages!

### Commands

1. `ls`
2. `cd`
3. `touch` and `mkdir`
4. `cp`
5. `mv`
6. `rm`
7. `sudo`

## Unsafe Commands (5 minutes)

### `sudo`

`sudo` -- or "super user do" -- runs the command that follows as the super user (i.e., 'root' or 'admin'). That means your computer will not prevent you from running the command and may not even confirm if this is what you actually want to do. This is of particular concern when the command may have destructive effects.

> Generally, you shouldn't need to run commands with `sudo` in this course. If you're not sure, ask an instructor.

### `rm`

`rm` -- or "remove" -- deletes files with no confirmation. There is no `trash` to recover removed files
from.  So use `rm` with caution.

You should especially use `rm -rf` with caution.

> Based on your knowledge of flags, what does `rm -rf` do?

## Keyboard Shortcuts (5 minutes)

The next three points are reasons not to hold down the arrow or delete keys.

### `ctrl-c`

Cancel whatever you were typing before. Abort!

### `ctrl-e`

Move cursor to the end of the line.

### `ctrl-a`

Move cursor to the beginning of the line

### The up and down arrows

Cycle through previous commands

### Tab completion

When typing a command that has a file as an argument, like `cd`,
type only the first few letters and hit the TAB key.

### Clear the screen

- ctrl-l
- command-k
- `clear`

## Closing

The commands we've covered in this lesson will probably account for 80% of your CLI usage. On the one hand, that means that learning them well and getting comfortable is really important; on the other hand, it's not a big universe of commands to learn and memorize.

Regardless of how much experience with the command line you have coming in to this class, your next step should be to get really comfortable with it - we're going to spend a lot of time in the command line over the next 12 weeks. That can mean practicing these commands more, almost like you would practice scales from music or drills from sports. That can also mean learning more about what else is capable with these commands.

### Go figure some stuff out

Getting comfortable in the command line takes practice. Once you do get comfortable, you'll find it possible to be extremely productive by just adding a couple of commands together.

The installfest script is a perfect example - your instructors wrote a single shell script that you can run to totally set up your computers for WDI. Ask your instructors about other shell scripts they wrote at previous jobs.

For the remainder of class, here are some things you can go try to figure out how to do to get more comfortable with the command line:

- **Review the commands we've covered in more depth.** Go through each and review the help and/or `man` page for each command. Type `man <some_command` (i.e. `man ls`) to view the man page. Use your arrow keys (up and down) to navigate through the man pages and `q` to quit.
- **Practice each command.** Over time, these common commands will become part of your muscle memory. Get there sooner by practicing. Navigate to your `sandbox/` directory and create a `cli-practice/` directory. `cd` into your new directory and practice the above commands 20 times each.
- **Customize your command line.** The sky is the limit here! You can change the font, the theme (colors), add emojis to your prompt, use a different terminal (many of your instructors use iTerm) or even use a different shell (Bash is the default shell, some of your instructors use [zsh](http://code.joejag.com/2014/why-zsh.html).
- **Create Bash profile aliases.**  You can alias common commands in bash. One common alias you'll see a lot is an `ll` command that will perform an `ls -a` (list all files). See if you can figure out how to create that alias (google is your friend). Another possible alias you could make is `trash`, a command that will move a file or folder to the system Trash bin. What other aliases could you make?
- **Review some more advanced commands.** Look up `grep`, `less`, `cal`, and `vim`. View the `man` pages or google them!
- **Learn some custom, advanced commands.** [`Z`](https://github.com/rupa/z) is a command line tool for quickly navigating and traversing the file system. See if you can figure out how to install and use it. [This may be helpful!](https://commandlinepoweruser.com/).

## [Homework: To Oz](https://git.generalassemb.ly/ga-wdi-exercises/to_oz)

### Submission Instructions

1. Go to the assignment's [issues page](https://git.generalassemb.ly/ga-wdi-exercises/to_oz/issues).
2. Click 'New Issue’.
3. Give it a title of `CLI HW (Your Name Here)`. Replace "Your Name Here" with your actual name.
4. For the description, copy paste the CLI commands you used to complete the assignment.

## Additional Practice / Bonus Material

- [Command Line Fu](https://github.com/ga-wdi-exercises/command_line_fu)
- [Kitchen Organizer](https://github.com/ga-wdi-exercises/kitchen_organizer)
- [Command Line Power User](https://commandlinepoweruser.com/)

## Bash Profile Aliases (Bonus Content)

You may have noticed during Installfest that we messed with this file: `~/.bash_profile`.

<details>
  <summary> <b>Q:</b> Based on the path, where is this file located?</summary>
  In the home directory (i.e., Users/your-name-here).
</details>

Essentially, we changed the `~/.bash_profile` to make your prompt into a better one!

There will be commands you will find yourself doing frequently. It might become a pain to type out these commands in full all the time. It would be really nice if we could shorten some of these commands... enter aliasing. Aliasing is really quite simple!

Let's open our  `~/.bash_profile` in atom and type in the following...

```
alias greeting="echo 'hello world'"
alias gs='git status'
alias sbx='cd ~/wdi/sandbox'
```

We can also design functions in bash to allow for arguments and options...

```sh
cdls () {
cd "$@" && ls;
}
```

> At this point you may be wondering what exactly "bash" is. Bash is a language we can use to interact with our computer via the shell (via Terminal or some other text-based interface).

### Make An Alias

Take the next five minutes to create your own alias and test it. If possible, alias something you think you'll find yourself doing frequently!

## Sample Quiz Questions

* Why would a developer prefer the command line over a GUI?
* Where can we find help for shell commands?
* Describe 4 bash commands for managing folders and files.
* Describe 2 unsafe commands.
* You are currently in the "code" folder in the below file tree. How would you get to the folder that contains "beach.png" using the command line?

```sh
home
├── documents
│   └── code
├── photos
│   ├── headshot.jpg
│   └── summer_vacation_2014
│       └── beach.png
└── videos
```

* **BONUS:** Write a command to list only files beginning with your first name. Label the parts of the command.

## Hungry for More?

* `grep`
* `cat`
* `less`
* `find`
* `cal`
* `vim` and `vimtutor`

[Linux Command](http://linuxcommand.org/) is a wonderful introduction to the command line. Macs are Unix systems and so very similar to Linux. Almost everything (everything I've found so far)

## Own your terminal

1. [Color your prompt](http://www.cyberciti.biz/faq/bash-shell-change-the-color-of-my-shell-prompt-under-linux-or-unix/)
  - It will be WAY easier to read
2. [Choose a theme](http://apple.stackexchange.com/a/92769)
  - Pick something you like to look at

## [iTerm2](https://www.iterm2.com/features.html)

Some instructors use iTerm2 as a terminal replacement.

Our favorite features include:

- A better, more readable font
- Hotkey support (full screen and tabs)
- Unlimited Scroll Back history

## Feeling Adventurous?

Bash isn't the only option. Check out zsh (http://code.joejag.com/2014/why-zsh.html) or fish (http://fishshell.com/)

