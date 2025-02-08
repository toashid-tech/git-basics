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

Let's start by 

## TODO Adding changes to your local repository

## TODO Uploading changes to GitHub

## TODO Restoring some changes

## Summary of commands:

- `git clone` creates a brand new copy of a remote Git repository.
- `git pull` downloads the new changes (new commits) **from** the remote
  repository.  We have not used this command in this tutorial.
- `git add` marks some files as changed for the next commit.
- `git commit -m 'commit message'` creates a new commit.
- `git push` uploads all the new commits **to** the remote repository.
- `git restore foo.txt` undoes uncommitted changes to `foo.txt`.
