# Git Fundamentals
By [John Cotton](https://github.com/thejohncotton)

---

![XKCD Git comic](https://imgs.xkcd.com/comics/git_2x.png)


### Note:
This is intended to assist an in-person workshop and is by no means exhaustive or complete (Don't judge me).

## Getting Started

This workshop assumes that you have a [github](https://github.com) account, a [netlify](neflify.com) account and have made your way through the [intro to cli/version control](cli-and-git-tutorial.md) workshop.

---
## Clone

Cloning is a fast way to create an identical copy of a repository.

If you have already created your own hello app please clone your repository. If you haven't please feel free to use mine (You will need to update your remote branch address if you want to be able to push changes)

Navigate to the appropriate directory and clone this repository (or your own repository): 
`git clone https://github.com/thejohncotton/hello.git`



You now have a copy of the hello repository:

`cd hello`

`ls`

Expected outcome:
```/
index.html
readme.md
```


---
## Branch

A common git workflow is to use a new branch per feature.

For example, lets add a new about page to our demo project.

`git checkout -b feature-add-about-page`

This creates a new branch for our feature that contains the code specific to this feature and checks out that branch.


`git status`
``` 
> On branch feature-add-about-page
> nothing to commit, working tree clean
```
`git branch`
```
>* feature-add-about-page
>  master
```

Let's add a basic about page for our feature now.
1. Add the about directory:
    `mkdir about`
1. Add the index page for about:
    `touch about/index.html`

1. Add some content to your about file in your text editor or simply 'echo' some placeholder content:
`echo Hello About >> about/index.html`

Now that this is feature complete, let's commit the code.

`git add .`
`git commit -m "WIP add structure for about page"`

### Differences in Branches:
Now that we have committed our code on the feature branch, let's compare the differences between our feature branch and the master branch.
`ls`
```
>  about  index.html  readme.md
```

`git checkout master`
`ls`
```
> index.html    readme.md
```

We can all so check the `diff` between branches
`git diff master feature-add-about-page`

```git
diff --git a/about/index.html b/about/index.html
new file mode 100644
index 0000000..bcf5e83
--- /dev/null
+++ b/about/index.html
@@ -0,0 +1 @@
+Hello About
```
---
## Rebase

Often when you are collaborating on a codebase, the master branch will change out from under you. i.e. Someone else is working on a feature and gets their code merged before you. To avoid losing functionality you can simply rebase the new master branch.

Let's make a small change to master:

`git checkout master`
`echo small change readme.me`

`git status`
```git
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   readme.md
```

`git add .`

`git commit -m "small change"`
``` git
[master 466976f] small change
 1 file changed, 1 insertion(+), 1 deletion(-)
```

`git checkout feature-add-about-page`
`git diff master`
```git
diff --git a/about/index.html b/about/index.html
new file mode 100644
index 0000000..bcf5e83
--- /dev/null
+++ b/about/index.html
@@ -0,0 +1 @@
+Hello About
diff --git a/readme.md b/readme.md
index a9d97a1..5e1c309 100644
--- a/readme.md
+++ b/readme.md
@@ -1 +1 @@
-Hello Worldsmall change
+Hello World
\ No newline at end of file
```

Now let's rebase the newest additions from master

`git rebase master`
```git
First, rewinding head to replay your work on top of it...
Applying: WIP add structure for about page
```
`git diff master`
```git
diff --git a/about/index.html b/about/index.html
new file mode 100644
index 0000000..bcf5e83
--- /dev/null
+++ b/about/index.html
@@ -0,0 +1 @@
+Hello About
```

### Pull Requests (optional for the purpose of this workshop)

A common step in this workflow now would be to push this code to github and issue a pull request.

You can start this pushing to a remote branch i.e.

`git push origin feature-add-about-page`
```git
Enumerating objects: 9, done.
Counting objects: 100% (9/9), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (7/7), 594 bytes | 594.00 KiB/s, done.
Total 7 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), done.
remote:
remote: Create a pull request for 'feature-add-about-page' on GitHub by visiting:
remote:      https://github.com/thejohncotton/hello/pull/new/feature-add-about-page
remote:
To github.com:thejohncotton/hello.git
 * [new branch]      feature-add-about-page -> feature-add-about-page
```

Then head to the repository on github and create a new pull request.

---

## Merge

### Local
Now that our feature branch is rebased with master we can safely merge our code:

`git checkout master`
`git log`
```git
commit 466976f34ab9a53a8cb7730406579453a1f0d591 (HEAD -> master)
Author: John Cotton <john@1080people.com>
Date:   Mon Jan 20 16:41:46 2020 -0500

    small change

commit 72578b85d97bdeac51127a7e0f241017faebd069 (origin/master)
Author: John Cotton <john@1080people.com>
Date:   Mon Jan 20 16:09:35 2020 -0500

    add content
``` 

`git merge feature-add-about-page`

```git
Updating 466976f..6542abe
Fast-forward
 about/index.html | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 about/index.html
```

Now our master branch contains all of our feature code!

### Merging the Pull Request via Github
It is also possible to simple merge the Pull Request we made in the step above. Then in order to get our latest code from our remote branch, we would need to run `git pull origin master` to update our local repository.

## Reset
Let's say that we want to completely reset our repository to the initial state before we made our feature changes today.

We can simply copy the SHA from the log and use the reset command. i.e.
`git checkout master`
`git log`
```git
commit 6542abe5e721526dbd886e283e3b672bf750cf6e (HEAD -> feature-add-about-page, origin/feature-add-about-page, master)
Author: John Cotton <john@1080people.com>
Date:   Mon Jan 20 16:29:13 2020 -0500

    WIP add structure for about page

commit 466976f34ab9a53a8cb7730406579453a1f0d591
Author: John Cotton <john@1080people.com>
Date:   Mon Jan 20 16:41:46 2020 -0500

    small change

commit 72578b85d97bdeac51127a7e0f241017faebd069 (origin/master)
Author: John Cotton <john@1080people.com>
Date:   Mon Jan 20 16:09:35 2020 -0500

    add content
```


`git reset 72578b85d97bdeac51127a7e0f241017faebd069 --hard`
```git
HEAD is now at 72578b8 add content
```

Now our master branch is back in it's initial state before we made the small change and merged the feature branch.

`git log`
```git
commit 72578b85d97bdeac51127a7e0f241017faebd069 (HEAD -> master, origin/master)
Author: John Cotton <john@1080people.com>
Date:   Mon Jan 20 16:09:35 2020 -0500

    add content
```