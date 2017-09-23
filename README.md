# A Linux Dude's Setup for Windows

I recently got a second-hand XPS13 laptop, and as a software developer,
it is my proud duty to tinker with it and turn it into a decent
development environment.

I'd like to list how I've managed to create a development environment
setup in Windows 10, trying to replicate my Linux environment at work.

Here's a high level view of the things I did while trying the task:

1. Installed **Windows Subsystem for Linux**
2. Setup terminal.
3. Setup my favorite text editor, **vim** ;)
4. Setup my favorite package manager, **brew**
5. Install all the things!

## Background

Initially, I did all this to get an **Elixir** development environment going.
Note that I'm a complete beginner in this particular language so some
things I did might trigger the developer OCD within you. Corrections and
suggestions are very much appreciated!

My setup at work is as follows:

```
OS:                 Goobuntu
WM:                 Unity (grid workspaces rock!)
Text Editor:        Sublime Text / vim
Shell:              Fish
Version Control:    git5 / git
Languages:          Go, Typescript, Python, HTML+CSS+JS, Shell Script
Frameworks:         Angular 2, AngularJS, jinja, Django
Platforms:          AppEngine, #plx, Borg
DBs:                CloudSQL, SQlite3, Datastore
```

As much as I would like to replicate my work setup, I'll replace some of
these tools with a similar thing just so I could learn a few things here
and there.

## Installing Windows Subsystem for Linux

When I first got the laptop, I immediately searched for WSL... and became
disappointed when it's not even in the **Turn Windows features on or off**[^1]
prompt.

That's when I learned that my Windows 10 copy wasn't updated for a loong
time, and that WSL came to windows in the Creators Update.

> > M: I tried updating Windows 10 to the latest, but there's still no WSL
> >    option in **Turn Windows features on or off**. Now what?
> Yeah me too. I did try to update my Windows copy to the latest but I guess
> it's stuck in the stable (ooold) branch?
> So what I did was to turn on *Release Preview* builds within the **Windows
> Insider Program**[^2]. And then allow Windows to update.

Select on **Developer Mode**[^3] in the **For Developers** setting.

After all that, an entry called **Windows Subsystem for Linux (beta)** should
appear in the **Turn Windows features on or off** prompt.

[*^1]: Press **Windows** key, type in: `Turn Windows features`. It should appear
at the top of the list.

[^2]: Press Windows key, type in: `Windows Insider Program`. It should appear
at the top of the list.

[^3]: Press Windows key, type in: `For Developers`. It should appear at the
top of the list.

## Preamble Package Installations

Just so I won't litter the next sections with `sudo apt-get install` commands,
I'll just list all the required `apt` packages. Run the ff:

```
sudo apt-get install curl git zsh cmake ruby build-essentials libxml-perl
```

Now, some of these you probably think you won't need. But trust me, you'll
probably need them once you start tinkering on your own.

## Setup Terminal

Most of these are ripped off from [Mikhail's Excellent Setup](https://evdokimovm.github.io/windows/zsh/shell/syntax/highlighting/ohmyzsh/hyper/terminal/2017/02/24/how-to-install-zsh-and-oh-my-zsh-on-windows-10.html)
for **Oh My Zsh**. You can go there for a more complete set of instructions.

1. Open `bash.exe`[^4] and type the ff:

```
sudo apt-get install curl git zsh
curl -L https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh | bash
```

These install `curl, git, zsh` and executes the installer for **Oh My Zsh**.

[^4]: Press Windows key, type in: `bash`.

2. Next, we install some cool `zsh` plugins. Run the ff:

```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
```

And then edit `~/.zshrc`:

```
plugins=( [plugins...] zsh-syntax-highlighting zsh-autosuggestions)
```

Load your new .zshrc:

```
source ~/.zshrc
```

3. (Optional) Hyper Terminal

This is optional, but you might want to download **Hyper Terminal* [Link](https://hyper.is/).
It's an awesome terminal compared to the default command prompt in Windows.

Once installed, edit `%USERPROFILE%/.hyper.js` and change the line:

```
shell: '',
```

with:

```
shell: 'C:\\Windows\\System32\\bash.exe',
```

Now, when you try opening `bash.exe` again, it'll instead run `bash` within
the **Hyper Terminal**.

## Setup **vim**!

**vim** 7.4+ should be installed by default when you first start **WSL**.

Now, I would like to introduce you to **Steve's (spf13)** awesome full packaged
[vim distribution](https://github.com/spf13/spf13-vim). You probably won't
need to tinker with you vimconfigs after installing this :)

Run the ff:

```
sh <(curl https://j.mp/spf13-vim3 -L)
```

## Setup Package Manager

`brew` is a cool little package manager for **Mac OS**. It's like `apt`, but
has more bleeding-edge packages.

It's also available in **Linux** via `linuxbrew`. To install, run the ff:

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Linuxbrew/install/master/install)"
```

## All the (Dev) Things

Below are programming tools that I've installed via `brew`:

```
brew install go
brew install node
npm install -g typescript
brew install elixir
```

> Upon installing **Elixir** via `brew`, I encountered a missing XML::Parser
> package for perl. This is super weird and I can't even configure cpan to
> install it properly for me. So what I've tried is to install a pre-built
> XML::Parser perl lib for me by installing a package from apt. Which is why
> I asked earlier to install `libxml-perl`.

## Home Folder Structure

> This section is very very subjective. I chose to let it be here as it is
> in my original draft.

This where all personal nerdy things go. Make sure to maintain proper
folder structure. Here's how it currently looks:

```
~/Documents
~/Downloads
~/Github
```

## Things of Note

1. I've tried to install `byobu` as it's my go-to window manager in the
   terminal. However, as of time of writing, there is a bug in **WSL** that
   won't let `bash.exe` accept function keys. Even if it's wrapped in
   another Windows terminal. Link to [bug](https://github.com/Microsoft/BashOnWindows/issues/1496).

   Fortunately, `hyper.js` allows split views (Ctrl+Shift+D) and tabbed
   (Ctrl+Shift+T) terminals. And it's amazing, as I can scroll each view
   with my touchpad!

## Conclusion

> TODO(ncapule): This guide  is a work in progress. And the first time this
> author would create one. Please improve!

I guess that should be all of it. All in all this setup took me about 4
hours due to the atrociously slow internet speed here in the Philippines.

I hope this guide contributed at least some points into the (dev) world.

Bye!
