# Unix Shell Session 1

## What is a "shell"?

A shell is an interface between you and your computer. You normally use a GUI (graphical user interface) which consists of a combination of clicking buttons and icons, typing into prompts, and navigating visual representations of file systems (among other things as well) in order to do things on your computer. A shell is not a "graphical" but rather a text-based setting in which you can do things on your computer. It's called a shell because it is a "shell" around the internals of your computer. 

A shell basically takes in the commands you type with any arguments/parameters and dispatches the appropriate process(es). A command line interface is an interface to your computer that uses a shell. This is also called a terminal. Although there are distinctive differences between these terms, for our purposes a "shell", "command line interface", and a "terminal" will all mean the same thing.

Think of the command line as a text-based "Finder" (on Mac) or "My Computer" (on Windows) on steroids. You can navigate through folders, open files, copy files, delete files, move files, etc. However, there are also TONS of commands you can execute on these directories or files that are really helpful. For example, you can search through a directory to find all files that contain a certain piece of text using the "grep" command. Also, the code-like syntax of the command line input is really helpful. For example, you could execute a process on all files that start with some prefix or end with some suffix all at once with one command.

This session aims to introduce you to the basics of using the command line, and this session series aims to make you fully competent with using the command line for software development both in the professional workplace and for your own projects (class and individual). 

## AWS EC2 Background Info

Amazon EC2 (Elastic Compute Cloud) is an AWS service that allows users to create virtual computer instances and access them over the cloud.  AWS manages the hosting of your instances (they own the hardware, deal with all of the headaches of maintenance, CPU optimization, and software updates) so that you can just remotely connect to your instance through your terminal and the internet. This stands in stark contrast to something like [virtual box](http://virtualbox.org) which cuts out part of your own computer's hardware and provisions it for your virtual box.

We will use EC2 instances and interact with them remotely using just the command line. However, first we will create and launch the instance from the [EC2 console page](https://console.aws.amazon.com/ec2/v2/home?region=us-east-1). 




## Create and Launch an EC2 Instance

AWS EC2 gives you the option of choosing between a wide variety of hardware and software for your virtual instance. You can even create huge instances with lots of cores and an absurd amount of memory. This comes at no cost to your own hardware, since it is all hosted remotely and you just connect to your instance through the command line. This is remote connection to your instance is called "ssh", or secure shell. It is a command line/shell interface to your instance, securely connected over the internet.

* Once you have set up your AWS account (see [instructions](http://vandyapps.club/post/2016/09/01/unix-shell-session-setup-instructions)) go to the [EC2 console page](https://console.aws.amazon.com/ec2/v2/home?region=us-east-1) and make sure you are in the North Virginia/US-East-1 region (this is the region closest to Nashville, so the latency between you and the instance will be minimal)
* Click on the blue "Launch Instance" button
* Choose Ubuntu as your operating system
* Choose a general purpose t2.micro instance type (this should be selected by default)
* Click "Review and Launch"
  
Stop on the page you are now on!

We need to change the security settings on your instance so that you can ssh into your instance without any networking headaches. So let's configure your instance to allow ssh connections from any IP address (this is not great security, but it is simple and we don't need to worry about security on our instances for these sessions).


* Click edit security groups
* under source, make sure it says “anywhere” and 0.0.0.0/0
* Click Review and Launch
* Click Launch

Now we need to create a key-and-lock pair for our instance so that when we ssh to it our computer can present the key and successfully authenticate our connection.

* Click "Create a New Key Pair"
* Give it any name you want
* Click "Download Key Pair" and save it somewhere on your computer
* Click "View Instances"
* Give your instance a name in the Name field

Now we need to change the permissions on that file to make it restricted. If you're on windows, right click the file and go to Properties -> Security -> Edit and change the permissions to read only. If you're on a Linux-based OS let's do it on the command line:

* Open your terminal
```
cd path-of/folder/that-holds/your_key
```
CD, or "change directory" moves you from your current directory to the new directory you specify. This is like clicking on a folder in Finder/My Computer except that you can go straight into a nested folder by providing the full path. Then, we will use the LS command, or "list" to show the contents of the directory we are now in. However, we are here to change the permissions to a file, so let's type:
```
ls -l
```
This will also show the read/write/execute permissions of all the contents of the directory we are in. Now we want to use the CHMOD command to change the permissions on our file. The structure of the command is:
```
chmod <number> <file to be chmodded>
```
The number here (always 3 digits) represents a certain permission level. The number can be determined as follows: Each digit corresponds to a level of user, i.e. (normal)(privileged)(root). The number to be placed in each digit is the decimal equivalent of the binary representation for the deisred permissions in the format read|write|execute, where 1 represents a "yes", or "permitted", and a 0 represents a "no", or "not permitted". So we want everyone do be able to read this file, and that's it. No writing, no executing. So that would result in:
* First digit: (1|0|0)
* Second digit: (0|0|0)
* Third digit: (0|0|0)

Now we drop the fluff and convert from binary to decimal to a chmod argument number:
100 000 000 -> 4 0 0 -> 400.

If this is still unclear, check out [this tutorial](http://www.tutorialspoint.com/unix/unix-file-permission.htm) out for more clarity.

Now go back to your [console page](https://console.aws.amazon.com/ec2/v2/home?region=us-east-1). Find the public IP address of your instance, and once the instance state goes from “pending” to “running”, try sshing in. Linux-based OS users: open your terminal and type
```
ssh -i path-to/ssh_key/file ubuntu@<public IP address>
```
For example:
```
ssh -i unix-shell-sesh.pem ubuntu@54.166.96.4
```

And now you are connected to your VM!
