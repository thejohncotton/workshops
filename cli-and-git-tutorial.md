# Introduction To CLI and Version Control

Become a power user by typing more, clicking less, and build programs inside development environments that emulate actual web servers by learning about The Command Line Interface. And keep your source code safe, maintained, and manage collaboration by learning Version Control.

## Housekeeping

This is not a course for experienced developers as much as it is a collection of exercises to introduce serious learners to key concepts.

## Installfest

### Windows Users

1. Head on over to [Babun's github page](http://babun.github.io/) and download
2. Download / run the installer
3. The install may take several minutes so move on to  Create Accounts.

### Mac / Linux users
No installation Necessary! Open up the Terminal Application and move on to Create Accounts.

## Create Accounts
If you don't have one already, create a [Github](https:github.com) account.


## Navigating your computer's file system
You can go your entire life using a computer without having to type commands. You are used to interacting with a system of graphics known as a GUI (*pron. gooey*) short for Graphical User Interface.

The GUI is an abstraction of the way humans interact with a computer. Your average user does not have to remember complex (or even simple) commands. This is great for general users, but developers, administrators, and devops professionals need to access more components of the computer / server, and we can do this swiftly using the CLI.

## The Tree Model
When interacting with the CLI it is important to have a mental model of your computer's file system. Mostly you will encounter the system referenced as a tree. Let's have a look at the following project (don't paste this in your terminal).

### A baby website tree

    root     
    ├── index.html
    ├── css
    │   └── style.css
    └── js
        └── app.js

Notice the word root. The root directory *(folder)* contains an index.html file, two subdirectories css, and js. That each contain a file.

**We can navigate this system of files using paths.**
In the above example if we wanted to reference the app.js file, we can't just type 'app.js' we need to provide more detail as to where app.js is, we can use it's path. Which is 

    root/js/app.js
---
## Moving around without graphics

##### Now that we know about trees, roots, and paths let's practice getting around. Here are a few commands you can use to get started.

 *Be sure to practice typing these on your own rather than copy and paste (I know, I know, but we're building skills right?).*

**Where Am I?** *(Print the working directory)*

    pwd

**What is in this folder?** *(List the contents of this folder)*

    ls
**Take me back to my user directory**

    cd ~

**Make a new directory called CLI Workshop**

    mkdir cli-workshop


**Change directories into cli-workshop**

    cd cli-workshop

**Move back one directory**

    cd ..
    
**Move into cli-workshop using path from user directory**

    cd ~/cli-workshop

---

## Look mum, no GUI!

**Quiz time!**

1. Which command do you use to print your current location on a new line?
2. Which command do you use to create a new folder?
3. Which command do you use to change locations?
4. Which command do you use to list the contents of a folder?

## Echo (echo)
 
Let's try a different kind of command.

    echo hello

The echo command is a simple way to tell the terminal to echo your input on a new line. Pretty useless right? 

Run the following command.

    echo hello > greeting.txt

Now type

    ls

We have just created a new file called greeting. Let's open it.

    open greeting.txt


Very cool (You may close it now). What if we want to add another greeting to this file without using a text editor?

    echo hi >> greeting.txt

Let's open our greeting file again

     open greeting.txt

What happened? Well, there is a small difference between **>** and **>>**

Think of **>** as *write*, and **>>** as *append*


#### Removing a file

    rm greeting.txt

#### Removing a folder and it's contents

    rm -r folder
Note the *-r* here. This means to remove with recursion the folder, and everything inside of it.

---

### A quick Bio

Let's use echo one more time to write a short biography about yourself. We'll build on this later and make it pretty. Now let's get the content flowing.

    echo "About Me:" > about.txt

Now use the same command with *>>* to add a few things about yourself.

Like your name.

    echo "My name is John" >> about.txt

Add something interesting about yourself:

    echo "I like music" >> about.txt


---
# Version Control
Right now our project is very basic. But we plan to build and make changes in the future. Let's turn our project folder into a git repository that will track our changes and allow us to organize them into meaningful sets of changes.

#### Configure git user settings
Time to set the username for git on our system. Be sure to use the same email address you used with your github account.

    git config --global user.email "you@example.com"

Next we need to set the name for our user.

     git config --global user.name "Your Name"

#### Initialize

    git init

We just initialized git. This means that we can now monitor and track the changes in our code. 

#### Let's check our status

    git status

#### Let's add our files into staging

    git add about.txt

This command adds our about.txt file into staging.

We could also add all changes in our directory using

    git add .

The . in this command means we want to add all files inside  our cli-workshop folder.

#### Check status again

    git status

Notice the green? Cool right?


Add a new line to your about.txt file
   
    echo "I have two dogs" >> about.txt

#### Check status again
    git status

#### add those changes

    git add .



#### Registering changes as a commit
A commit is a way to register changes in our code that go together. We want to commit the changes into our history so we can fully restore our projects back to the state of these commits later or to tell other people about what changes we made to our code.


#### Commit

    git commit -m "initialize and add about file"

We've successfully added our commit!

#### Check status

    git status

You should see something like: 

    On branch master nothing to commit, working tree clean


There is one more important step in establishing our repository. 

#### Check status of remotes

    git remote -v

We can use a remote to store a version of our repository in the cloud.

Setup the remote repository:

1. Navigate to [github](https://github.com) and login if necessary
2. Create a new repository called 'cli-workshop'
3. Uncheck the "initialize with Readme.md" checkbox
4. Click the green create button

We've successfully created the remote repository, now it's time to connect it with our local project.

1. Click the green 'Clone or Download' button
2. Copy the address from the clone with https modal

With the url in your clipboard, type the following command followed by pasting that url .
    
    git remote add origin

For example:

    git remote add origin https://github.com/thejohncotton/repository.git

#### Check the status of our remotes

     git remote -v

Double check to confirm the url of your remote is correct.

#### Pushing changes to the cloud

We are now ready to send our local code to github.

    git push origin master

Where git push is the command, and origin is the remote (that url we pasted in) and master is the branch (a little beyond the scope of this workshop).

You may be prompted for your username and password. Enter those to continue.

Head back over to [github](https://github.com) and refresh your repository.

*Voila*

Your code is now connected to the cloud!