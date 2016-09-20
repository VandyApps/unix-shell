### Unix Session 3: vim

Today we are going to add a bunch of helpful features to vim to make it a useful IDE.

#### .vimrc File
The .vimrc file is a file that vim uses for configuration. This file doesn’t come built in with vim, and unless you create one yourself, vim will just have its simple, boring, default configuration. This file should be located at your user root ~/, so let’s create it and open it up there with
```
vim ~/.vimrc
```
Right now this is an empty file, and vim will basically read it as a script of instructions whenever vim is opened. So let’s add
```
nmap <space> :
```
to the file. This maps the spacebar key to the colon input, so that you can do all of your vim commands like :q, :w, :e, etc. by typing spacebar-q, spacebar-w etc. I just think spacebar is easier. If you disagree or want to change it to something else you find fits better, go for it.

NOTE: since the .vimrc file starts with a “.” it will NOT show up when you type “ls”. You need to type “ls -a” in order to see dotted files.

Now save and quit (for the last time with actually typing :wq), and upon opening again, vim will have the configuration you specified. I have provided a bunch of helpful .vimrc configurations on our github, so let’s make sure we’re up to date with the [Unix Shell Session Github Repository](https://github.com/VandyApps/unix-shell/):
* cd to your folder (probably called something like unix-shell) that is linked to the unix shell session 
* then type “git fetch” and then “git pull” to update your folder
Now you should have a folder in your directory called “vim-setup”. This contains some helpful pre-written .vimrc configurations.

Now let’s copy the contents of the init_config file into our .vimrc from inside vim. We can do this pretty quickly with some vim key-bindings:

* open the vimrc file
```
vim ~/.vimrc
```
* also open the init_config file as another buffer from within vim. :e <filename> is the vim command for this. :e stands for “edit”
```
:e ~/unix-shell/vim-setup/init_config
```
Now we want to highlight all of the lines in this file except the first one, copy them, and paste them in the previous file, ~/.vimrc:
* shift-v selects an entire line
* shift-G moves your cursor to the bottom of a file (and gg moves it to the top)
* y copies the selected text
* bp moves you back to the _P_revious _B_uffer you were in (which should be ~/.vimrc)
* p pastes your text that’s on vim’s clipboard

Once you have all of that content in your .vimrc, save and quit vim. These configurations are mostly things you will never notice, since they make vim behave as you would expect a text editor to behave.

So now that we have these initial configurations, let’s go a step further. There are tons of plugins for vim that make it even more robust. We could go online, download them individually, manually handle updating them, and manually connect them to vim and its .vimrc. However, this is a lot of work and fortunately package managers have been written just for this purpose. Just like APT-GET is a nice tool that makes downloading of command-line tools really simple, [Vundle](https://github.com/VundleVim/Vundle.vim) makes dealing with vim packages really nice. There are also other ones out there but we will use Vundle.

#### Plugins and Vundle
Before we pull down Vundle, let’s make a directory where we are going to store all of our plugins that we are about to get:
```
mkdir -p .vim/bundle
```
The -p option allows for us to make a nested folder, since the .vim folder doesn’t exist either. If we didn’t supply the -p option here, we would get an error message saying
```
mkdir: bundle: No such file or directory 
```
So cd into .vim/bundle, and now we want to pull down the Vundle code into this folder using git clone:
```
git clone https://github.com/VundleVim/Vundle.vim
```
On [Vundle’s Github page](https://github.com/VundleVim/Vundle.vim) there is an explanation of how to set this up in case you have any problems.

Anyways, now that we have Vundle, we can simply add the github link of a vim plugin that we want in the .vimrc file, and Vundle will install it and keep it updated. So here are the plugins we are going to add:

* [YouCompleteMe](https://github.com/Valloric/YouCompleteMe), an auto-completer for all of your auto-complete needs
* [NerdTree](https://github.com/scrooloose/nerdtree), a plugin that shows your directory tree structure for easy directory navigation/file opening from within vim
* [DelimitMate](https://github.com/Raimondi/delimitMate), a plugin that automatically creates closing punctuation—  “, ], }, ) — upon creation of the opening quote/bracket/etc.

The code for how this should look in your .vimrc is in the “plugins” file in your unix-shell/vim-setup folder (i.e. at ~/unix-shell/vim-setup/plugins). You should copy and paste these contents into your ~/.vimrc file in the same way you did previously.

Now write and quit, and reopen vim by simply typing vim into the command line prompt. Then
```
:PluginInstall
```
will bring up a window from Vundle and it will go through and install all uninstalled plugins that are listed in the vimrc. They should all install quickly, except for YouCompleteMe, which should take about 30 seconds.


#### YouCompleteMe and Manually Building Directories

So YouCompleteMe will not work right off the bat. It needs to be compiled. In other words, the code that you pulled down from GitHub via Vundle when you ran PluginInstall still needs more things to be done with it in order for it to run. All of this configuration and installation is done with the install.py file in the YouCompleteMe folder, which is located in the ~/.vim/bundle directory.
So let’s go there:
```
cd ~/.vim/bundle/YouCompleteMe
```
we want to run the install.py file, but if you read the installation steps on the [YouCompleteMe Github page](https://github.com/Valloric/YouCompleteMe), you will notice that it specifies that ubuntu users should have the following command line tools before running install.py:
* build-essential 
* cmake 
* python-dev
* python3-dev

So let’s install those real quick before we go any further (and if any of them are already installed, then they will just get skipped over):
```
sudo apt-get install build-essential cmake python-dev python3-dev
```
As you can see, we can call apt-get install from anywere, we don’t have to be at ~/. Also, we can list a bunch of packages in a row and it will install all of them. This is equivalent to doing “sudo apt-get install” to each one in the list individually.
So now that we have all of those command line tools installed (YouCompleteMe will in turn use them to build/install itself), now let’s execute the install.py file.

If you recall from last week’s session, we ran python files by typing
```
python <name of file>
```
You can also make python files directly executable. If you notice, the first line of the install.py file is
```
#!/usr/bin/env python
```
This specifies which python the file wants to use if it is executed. So we can just run
```
./install.py
```
and it will build YouCompleteMe. This will take a few minutes.

Once this is done, we can now open up any file with vim and YouCompleteMe (along with all of the other plugins and configurations we’ve done) will be active. However, you should be getting some annoying error messages from YouCompleteMe upon opening up vim.

### Debugging
Debugging is probably the most important command line skill to have. This instance is a nice example of a general issue you will face all the time on the command line — stuff doesn’t work right out of the box. Some people get really frustrated by dealing with errors on the command line, but you should learn to EXPECT errors everywhere all the time, and be pleasantly surprised when there are none. And then treat the puzzle of fixing your error as a challenge or a puzzle. Google is your best friend.

I’ve already done the work for you in this case, as you can find details on the issues at [this YouCompleteMe issue ticket on GitHub](https://github.com/Valloric/YouCompleteMe/issues/2335) and the code for the solution [here](https://github.com/Valloric/YouCompleteMe/pull/2337/commits/55cc3e2d43c246cb93f71136f63c6180fd5ebf20).

Basically all we need to do is add the code from [this file](https://github.com/Valloric/YouCompleteMe/pull/2337/commits/55cc3e2d43c246cb93f71136f63c6180fd5ebf20) to the beginning of the last function in the ~/.vim/bundle/YouCompleteMe/install.py file.


### Final Touches
Python-mode is also a really helpful vim plugin for python, and since we will be using it here, let’s install it. It does syntax and error checking whenever you save your file, so you can see errors really easily. It also does A LOT of other stuff. But that’s my favorite feature. So let’s add
```
Plugin ‘klen/python-mode’
```
and re-run PluginInstall to get python-mode installed. Now we should see all of the awesome auto-completion, syntax and error checking, and even a colored line at column 80 to show where your code line should stop.

Let’s also add
```
nmap ? :NERDTree<CR> to .vimrc
```
to our vimrc. Now when you type ? in vim you should see a nice graphical representation of your directory tree come up through which you can navigate and open files.

There is SO much more you can do with your vim configuration, and here are some places to start that can give you some ideas of how other people go about pimping out their vim:
* [Vim as a Python IDE](https://unlogic.co.uk/2013/02/08/vim-as-a-python-ide/)
* [spf13, the Ultimate Vim Distribution](http://vim.spf13.com)
