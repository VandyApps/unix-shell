## Unix Shell Session 2

In today's session we are going to learn:

* how to use the ubuntu package manager (apt-get)
* how to use git
* how to use vim for coding
* how to write a bash script
* how to personalize vim through your vimrc
* how to personalize vim through plugins

### Our Project:
For today's session we are going to build upon an existing project that can be found [on GitHub](https://github.com/VandyApps/unix-shell). This repository in there called "project" contains two simple python files that have some skeleton code and an empty .sh file. 

Our goal is to pull down this repository from GitHub using the git command line tool, modify the code in the .py files, and fill in the .sh file to execute each of the python files (using vim). Then we will update our modified files in the git repository.

Once we get to this point, you will have a basic understanding of how to use vim. You will also have a basic understanding of how NOT to use vim. You will have seen how some of the key bindings are annoying, and how vim is extremely lacking in IDE features. So, we will look in to how to customize vim to make it waaaaaaaaaaay better.

#### apt-get

So we want to pull down [this repository](in order to do this, we need to use the [git command line tool](https://git-scm.com/about). 

We can type 
```
which git
```
to show where the git executable is located on our machine. You will notice that nothing shows up when you type this. That means we need to install it. We could download the files manually from a web page and then manually install them, but that is too much work.

The Ubuntu command line comes built-in in with a package manager that allows us to install common commmand line tools really easily. Git is one of the manny command line tools installable with this package manager. 

Simply type 
```
sudo apt-get install git
```
hit "Y" when prompted, and git will be installed. Now if you type "which git" it should show you where the git executable file is located. However, you just need to type "git" from wherever you are on the command line and the executable will be called appropriately.

#### Git

Now that we have git installed, let's use it to pull down the repository mentioned above:
```
git clone https://github.com/VandyApps/unix-shell
```
and now we should have a directory on our machine named "unix-shell" with the same contents as those in the repository online.

So let’s cd into that directory:
```
cd unix-shell
```
and then list the contents to see what’s in there:
```
ls
```
And then we want to move into the “project” folder, since that’s where the files that we are going to modify are located:
```
cd project
ls
```
But we actually want to take these files and put them in our own directory, so each of you can make changes and track them and update them independently. So let’s go back to the root folder by just typing “cd” with no other arguments. Now let’s make a new folder for our work:
```
mkdir proj
```
And to copy all the files in the unix-shell/project/ directory into our proj directory, we can do:
```
cp unix-shell/project/* proj/
```
The * is a wildcard. This command is basically saying “copy all the files of any form in the unix-shell/project directory and put them in the proj directory and give them the same name.” Now if we type “ls proj” we should see all three files in the proj folder.

Now we need to set up a remote repository online that we can connect our local directory to. So go to github.com and click the plus button on the top right to create a new repository. Give it any name you want. Copy the link of the repository to your clipboard.

Then back on our “proj” folder, we need to conenct it to git. So type:
```
git init
```
and then 
```
git remote add origin <link to your repository>
```
Now they are connected. Since our directory is being tracked with git, any changes we make to any files here will be noticed. We can modify the files and save them locally, but in order to update the remote repository online, we will need to go through a few more steps.

#### Vim
Vim is a text editor built in to the command line, so in order to open a file with vim just simply type:
```
vim <name of file>
```
so let’s open up alphabet.py:
```
vim alphabet.py
```
This file is simply meant to print out each letter in the alphabet one by one. There is some code missing, though, so let’s fill it in. In order to type in vim, you need to first press “i” to get into “insert mode”. Only then will your button-presses be recorded as text input. This is because there are a lot of other things to do in vim, and they use the keys too.

So get into insert mode, add the appropriate code to the file, and press escape to exit insert mode. Then type
```
:w
```
to save your file, and
```
:q
```
to quit vim. To run a python file from the command line, simply type:
```
python <name of file>
```
so let’s run alphabet.py:
```
python alphabet.py
```
and you should see each letter in the alphabet printed out one by one.

So now we have modified the file alphabet.py. Git has tracked this, as we can see if we type
```
git status
```
It should show that alphabet.py has been modified. After we finish our work, we will use git to “commit” and then “push” all modified files, which basically means we will save them in the git cloud, and then overwrite the files on the remote repository.

But for now, we will leave it and keep on working. Let’s open up the file clock.py:
```
vim clock.py
```
and fill in the code to print out the time to the screen. Now save and quit vim with the command
```
:wq
```
“git status” should now show two modified files.

#### Bash Scripting
As we saw earlier, we can execute a python script by typing
```
python <name of file>
```
in the command prompt. Now let’s say for some reason we want to execute the alphabet.py file and then the clock.py file one after the other. We could type
```
python alphabet.py
```
and wait for it to finish, and then type
```
python clock.py
```
but this requires us to wait for alphabet.py to finish and then manually input the next command. Bash scripting can help us here!

Think of a bash script (*.sh file) as a list of terminal commands to do in order. For example, you could have a bash script that does a bunch of cd’s, ls’s, rm’s, etc. although that would be pretty boring. So let’s open up the script.sh file with vim and fill in some code to execute alphabet.py and then clock.py. Think of the language here as “terminal command” language, with each command+arguments separated by new lines. 

Once you have added the appropriate code to script.sh, :wq in vim to save and quit. “git status” should show this file as modified now. Now in order to execute script.sh, we just type
```
./script.sh
```
However, this won’t work right now, since script.sh is not set to be executable. You can see this if you type
```
ls -l
```
You should not see an “x” anywhere in the permissions description on the left side of the file. To change this and make the file executable, we do the following command:
```
chmod +x script.sh
```
and now script.sh is executable and you can run 
```
./script.sh
```
to execute it. This should print out the alphabet in order and then start printing the time immediately after.

##### Git Again
Now let’s save our changes with git. In order to tell git which files we want to update, we have to “git add” them. So you can do this one by one or all at once:
```
git add alphabet.py clock.py script.sh
```
and now if you type “git status” it should show those three files in green. Then, the “git commit” command updates all of the added files (commonly referred to as being “staged”) in the git cloud. And you need to provide a message with a little description of the updates you made:
```
git commit -m “Filled in code in python files and wrote in bash commands to execute them in order”
```
Now all of these files are updated in the git cloud, but in order to send them down onto the remote repository and update the relevant files, we need to call
```
git push origin master
```
Now we’ve updated our code locally, and pushed our changes to the remote repository!

#### Vim
So if you didn’t notice, the default key-bindings in vim are annoying. Let’s change them so they’re less annoying.






