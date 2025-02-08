# Git basics workshop walkthrough

This is part of the Git basics workshop created in Spring 2025 semester at the
University of San Francisco.

Before you start, make sure that:
1. You have a GitHub account and you are logged in to GitHub.
2. If you are on Windows, you are using WSL or Git Bash.
    - WSL would be the easier option to follow for this tutorial.
3. You have a terminal window open.

If you are creating a GitHub account right now, I suggest picking a
username that you would not mind putting on your resume when applying to jobs,
as putting your GitHub portfolio on your resume is pretty common.

## Git, GitHub, repositories, etc.

- **Git** is a version control system: it allows you to keep track of changes to
  the files in a project (e.g., a programming assignment or a report).  Each
  project you maintain under git is in its own **repository** (**repo** for
  short).  You can think of the repository as the folder that contains all your
  source code and change history.
- **GitHub** is a website that hosts git repositories and provides convenience
  tools.
  
## Setting up your Git username

You should set up your name and email on Git, so it can attribute the changes
you make to you. For this, you need to run the following commands:

```
git config --global user.name "Your name"
git config --global user.email "the email address you used when creating your github account"
```
  
## Creating an SSH key

**If you already created an SSH key, you can skip to the next session.**

You need to prove your identity to GitHub when you want to upload/download
changes to your private repositories.  There are a few mechanisms foor doing
this, we will use SSH keys.  SSH keys work by creating a pair of keys which can
encrypt/decrypt data together.  One of these keys is a private key, and the
other is a public key.  **YOU SHOULD NEVER SHARE YOUR PRIVATE KEY WITH ANYONE OR
ANY WEBSITE UNDER ANY CIRCUMSTANCE.**  The public key is the one you will give
to GitHub so they can use it to check if any requests are actually coming from
your machine.

On your terminal, run:

```
ssh-keygen -t ed25519
```

When you are prompted with

```
Enter a file in which to save the key (/home/YOU/.ssh/id_ed25519):[Press enter]
```

Just press return.  Then, you will be prompted with a password you can set for
your SSH key.  You can just skip creating a password by hitting enter.  This
part is up to you.  The terminal will not print anything while you are typing
the password.

After all of these steps, you should have the public key at
`~/.ssh/id_ed25519.pub`.

## Adding your SSH key to GitHub

**If you already added an SSH key to GitHub, skip to the next section.**

Use the `cat` command to see the contents of your SSH **public** key (the file
with the `.pub`) extension by running `cat ~/.ssh/id_ed25519.pub`.

You should see an output like:

```
ssh-ed25519 <some letters and digits>
```

Then, follow [this
guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
for how to add your SSH key to GitHub.

Once you are done, you should see your SSH key when you:
- Click your profile picture on top right,
- Open the **Settings** page.
- Go to **SSH and GPG keys** section.

## Forking this repository

First thing you need to do is to **fork** this repository.  This operation will
create a copy of the repository under your GitHub account, so that you can
modify your copy during the workshop.  In most CS courses at USF, you won't need
to fork a repository.  However, creating forks is pretty common when
contributing to open-source software.

**Read all instructions on this section before following them.**

To fork this repository,
1. Click the "**Fork**" button on the top right (which is in between the "Watch"
   and the "Stars" buttons).
2. In the next screen, you can choose where to store the repository, etc.  The
   default settings work for our use case, so you can just click the "Create
   fork" button.
   
After these steps, you will be directed to your copy of this repo.  You should
continue following this tutorial on that repo.  Make sure that the URL you see
is on your browser is `github.com/<your username>/git-basics`.

## Cloning this repository

**Make sure that you are viewing this page on your fork of the repository, and
you already added your SSH key to GitHub.**

1. Click the green **Code** button on this page.
2. Select the SSH option.
3. Copy the address of the repo in the textbox (it looks like `git@github.com:...`).
4. On your terminal, go to where you want to create your local copy of this
   repo.  That is, where you want to store your work on your computer.
5. Type `git clone ` then paste the URL, it should look like `git clone git@github.com:<your username>/git-basics2.git`.
6. Hit return.
7. If you set an SSH password, you will be prompted to enter that.

If everything went well, you should see an output that looks like:

```
Cloning into 'git-basics'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (3/3), done.
```

Now, go into this directory (`cd git-basics`).  Then, you can open this
directory on your file browser:
- On Linux, `xdg-open .`
- On macOS, `open .`
- On Windows, `start .`

## Where everything is stored

Git allows you to work on your own copy of a project and upload/download the
changes when working with others.  We will use it only for a solo project, but
some aspects of this collaboration-first design are already there:
- You have your copy on your computer.
- There is another copy on GitHub.
- Changes to one copy are not automatically synchronized to the other copy.

We will do the following to see how you can use Git for keeping track of changes
and having a backup for your code:
1. Making some changes.
2. Adding those changes to your change history.
3. Uploading the changes to GitHub.
4. Making more changes.
5. Undoing some changes.

## Making changes

Let's start by inspecting the status of our repository by running `git status`,
this is what we get:

```
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

- The first line tells us which branch we are on, which is not important for
  this tutorial (we will see what branches are used for in the next workshop).
- The second line tells us that we are up to date with the remote repo (the
  default name for the remote repo is `origin`), and all changes we downloaded
  are synchronized.
- The last line tells us that there is nothing new on our local repo that we
  haven't uploaded to GitHub yet.
  
As we just cloned the repository, this all makes sense.  Let's start by editing
an existing file: open `hello.txt` on your favorite text editor, add a new line
(for example, add a line that says `I am learning Git!`), and save the file.

When you run `git status`, you should see the following:

```
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   hello.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Most of the information is the same as before, but we can see that there is a
change that is not "staged for commit".  "Staged for commit" means that the
change is marked for the next item we will add to the change history (each one
of these items is called a **commit**).

Specifcally, we have modified the file `hello.txt` but we haven't marked that
change.

## Adding changes to your local repository

We will use the `git add` command to mark/stage/add changes for our next commit.

### Marking a change

Let's tell Git that we want to include the modifications to `hello.txt` in our
next commit:

```
git add hello.txt
```

Now, if we run `git status`, we will see something different:

```
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   hello.txt

```

You can see that the modification is now under the heading `Changes to be committed`.

### Committing changes

When we are committing changes, we need to provide a descriptive message for
what the changes are for.  For this tutorial, we will use short messages, but
these messages can be really long and explaining the motivation behind the
changes (e.g., a bug fix).

Let's commit our change:

```
git commit -m 'added a new line to hello.txt'
```

Here, the structure of the command is as follows:
- `git commit` is the command.
- `-m` tells Git what our commit message is (if we don't give it, Git will open
  a text editor to write it).
- The next argument `'added a new line to hello.txt'` is our commit message.

After running this command, you should see an output like the following:

```
[main 1ca7e93] added a new line to hello.txt
 1 file changed, 2 insertions(+)
```

On the first line, you can see the commit message, and on the next line you can
see a summary of the changes.

### Why split it into `git add` and `git commit`?

- `git add` allows us to slowly mark changes, and we can pick and choose what we
  want to add before creating a commit and saving everything in the change
  history.
- `git commit` bundles all these changes and saves them to the commit history.
  This operation is a bit more involved to undo, so the separation gives us some
  control.
  
For quick commits that change existing files, you can just use `git commit file1 file2 ... fileN -m 'commit message'`.

### Adding new files

Let's create a new file and add it to our repository too.  The workflow is the
same, but the status of the repository will be different.

Use your favorite text editor to create a file named `greet.py` with the following contents:

```python
print('Hello, world!')
```

Now, when we run `git status`, we see a slightly different message:

```
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        greet.py

nothing added to commit but untracked files present (use "git add" to track)
```

- The second line says that we have 1 commit we haven't uploaded to `origin`
  (the remote repo).  We will do that later.
- The last few lines mention that there is a file named `greet.py` that Git is
  not keeping track of.
  
Git does not keep track of new files by default, we need to manually add them.
This way, it is harder for us to accidentally commit things like `.class` files
or temporary files we created.

Let's add and commit this file:

```
git add greet.py
git commit -m 'Created a hello world program'
```

## Uploading changes to GitHub

We created and saved some changes, but we have not uploaded them to GitHub.  So,
if something happens to our computer now, all changes will be lost!  We can see
the number of changes we haven't uploaded via `git status`:

```
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

The second line says that we have 2 changes we haven't uploaded yet.  We can see
the details of the change history via `git log`.  When you run it, you should
see something like this:

```
commit 413cdffa69b146281beb524f03c69d0f9e352085 (HEAD -> main)
Author: Your name <your email>
Date:   Fri Feb 7 17:35:13 2025 -0800

    Created a hello world program

commit 547d605a39013cd0f057f8ca36050101998ccd85
Author: Your name <your email>
Date:   Fri Feb 7 17:31:32 2025 -0800

    added a new line to hello.txt

commit 88ab9ab735e4dcf3138f7de9ffaa05f0d0a3516a (origin/main, origin/HEAD)
Author: Mehmet Emre <memre@usfca.edu>
Date:   Fri Feb 7 17:02:56 2025 -0800

...
```

The top changes are the changes we made in this workshop.  You see that the next
change is already on GitHub, because there is `origin/main` next to it.  This is
how Git marks where each repository's most recent change is at.

We will use the `git push` command to upload all these changes.  After running
`git push`, you should see something like:

```
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 12 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 603 bytes | 603.00 KiB/s, done.
Total 6 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To github.com:<your username>/git-basics.git
   88ab9ab..413cdff  main -> main
```

Now, if you refresh this page, you should see the updated files in the file list
above this README.

## Restoring some changes

One crucial functionality of Git is that **it is a backup you can use for
changes**.  To test this, let's just delete `hello.txt`.  Run `rm hello.txt`
then `ls`.  You should see that it is no longer in the file list:

```
$ ls
greet.py  README.md
```

However, Git still remembers old versions of this file.  Run `git status`:

```
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    hello.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

You can see that the action of deleting `hello.txt` is not committed to Git
history, and Git even tells us how to undo that change: via `git restore`.

Run `git restore hello.txt`.  Voila! `hello.txt` is back:

```
$ ls
greet.py  hello.txt  README.md
```

## How often should you commit?

I suggest creating and pushing commits when you are done with a logical step
(e.g., when you are passing a set of tests, or when you implemented an aspect of
your assignment).  This way, you can rest assured that you have a rich history
of backups you can restore from, and you can browse through your earlier changes
more easily.

## Summary of commands:

- `git clone` creates a brand new copy of a remote Git repository.
- `git pull` downloads the new changes (new commits) **from** the remote
  repository.  We have not used this command in this tutorial.
- `git status` shows the status of the repository.
- `git add` marks some files as changed for the next commit.
- `git commit -m 'commit message'` creates a new commit.
- `git push` uploads all the new commits **to** the remote repository.
- `git log` shows the change history (you can also view it on GitHub).
- `git restore foo.txt` undoes uncommitted changes to `foo.txt`.

## Do I have to use the command line for all this?

No.  There are lots of Git wrappers (your favorite IDE/editor might have one
too).  We used the command line because
- different students have different setups, and
- the command line interface is ubiquitous.
