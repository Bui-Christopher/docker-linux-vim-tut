# 03 - Linux Files/Directories and Intro to NeoVim

## Prerequisites
This lesson assumes that you have a debian container running.
```docker run -d --name deb1 debian tail -f /dev/null```

This is a reminder of how to execute the `/bin/bash` command to hop into the debian container.
```docker exec -it deb1 /bin/bash```

## Resources
[LearnLinuxTv Youtube](https://www.youtube.com/@LearnLinuxTV/featured)



The following lessons will try to encapsulate additional topics beonyd docker. For example NeoVim and linux.
## Basic Linux

### Current Directory
Let's check our current directory by typing `pwd` on your host terminal. This is your current directory, for me it's: `/home/cookie`.
We can also check for what else is within our current directory with `ls`.

### Folders
Now let's try creating a folder and changing our current directory into that folder.
```
mkdir scripts
cd scripts
```

Examine our new current directory with: `ls` again. Nothing is there. Let's add a file and try again:
```
touch update.sh
ls
```

Quick recap, we checked our current directory with `pwd` and it's contents with `ls`. Afterward, we created a folder and entered that folder with `cd` and `mkdir`.
What happens if we type `cd` without specifying a directory?
Type:
```cd```

Looks like nothing happened? Let's see with `pwd`.

What a surprise! It looks like it returned us to our home directory, in my case it's `/home/cookie`!

#### Hidden Folders
Similar to how windows handles folders, there may be hidden folders.
In Unix systems, it's common practice to have hidden files/folders to start with a `.`.
Try typing `ls -a` to examine all current folders which may include hidden folders/files as well.

#### Practice
Try doing these tasks without looking at the solutions below. It would greatly increase the linux/docker learning speed.
To also get us acquainted and practcied with docker, let us instead utilize docker containers.
1. Create a debian container
2. Hop into the container's shell
3. Examine the current directory after executing `/bin/bash`
4. Create a folder named scripts
5. Create a file named update.sh within the scripts folder

```
docker run -d --name deb debian tail -f /dev/null
docker exec -it deb1 /bin/bash
pwd
cd
pwd
mkdir scripts
touch update.sh
ls
```

If you make an mistakes we can remove files and folders with commands such as
```
rm $FILENAME
rmdir $DIRECTORY

```

Great! What now?

### More Linux, Intro to NeoVim
Now that we've played with quite a lot of our linux directory commands, let's explore our next lesson: VIM (NeoVim).

Within a windows or other consumer operating system, editing files is fairly trivial. Place the mouse icon and double click the file you'd like to edit.
The operating system examines the file extension, and assumes what program to open the file with. Sometimes, we can modify the default program per extension.
When editing text documents for windows its usually `Notepad` and Mac is `TextEdit`.

How is this handled within a VM? How do I edit files when there's no mouse cursor? The terminal!
Similar to how pdf's are opened with pdf viewers or browsers, we will modify text documents with text editors.

Now, what text editor should we use? There's quite a lot to try:
- Nano
- Vi
- Emacs
- Vim
- NeoVim

Note: If you do a google search for `vi` google returns `emacs`. When doing a search for `emacs`, `vi` is returned.

There's lots of pros and cons of each editor, and I would bring personal preference and injustice when describing each editor.

I'm going to be using NeoVim in this tutorial, and that's that. Vi was an early created text editor, then came vi improved (vim), and now NeoVim.

Stay within the docker container in the following lesson.
#### Install NeoVim
So, let's install it on the debian container:
```
apt install neovim
```

I'm sure it failed. Don't panic. Let's try again.
```
apt update
apt install neovim
```

Let's break these commands down.
`apt update` Retrieves and updates the lists of packages. This is important to note that it doesn't explicitly update the packages on your VM.
Instead, it updates the lists of packages on your VM, so that you can try and download and install softwares like neovim.

To iterate again, your VM did not have updated lists that contained NeoVim, so we updated and were able to find and install the NeoVim package.

What exactly is a package? A package can be viewed as a package of software. It's how machines handle sharing software, and in our case, it's NeoVim.
It could be LibreOffice (open source version of Microsoft Office), Gimp, (open source version of PhotoShop), etc...

Now finally, what exactly is `apt`? Well, it's another program so like other programs we can try something we've done before with docker:
```apt --help```

It's a package manager. Similar to an android phone's Play Store or Apple's AppStore we have a Debian's `apt` package management.
I want to clarify that `apt` pertains to Debian as other Linux distro's like Arch may use `pacman` or RedHat utilizes `yum`.

If running a Mac computer, it's also similar to HomeBrew.

#### Learning NeoVim
It is out of scope to teach NeoVim. Essentially, open neovim: `nvim`
To quit neovim, enter these characters: `:q`

To continue it's best to learn NeoVim by reading the ******* docs. If you haven't heard it before, RTFD.

Enter the neovim software and run the `:help` command.
```
nvim
:help
```

The final task is to write `Hello World` within the `/scripts/update.sh` we created earlier. 

Of course we can skip NeoVim entirely and use nano, but Vim/Emacs is a standard which is worth practicing. Good luck!
