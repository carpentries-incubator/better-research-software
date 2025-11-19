---
title: Better start with a software project
teaching: 30
exercises: 30
---

:::::::::::::::::::::::::::::::::::::: questions

- What is a version control system?
- Why is version control essential to building good software?
- What does a standard version control workflow look like?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Set up version control for our software project to track changes to it
- Create self-contained commits using Git to incrementally save work
- Push new work from a local machine to a remote server on GitHub

::::::::::::::::::::::::::::::::::::::::::::::::

In this episode, we will set up our new research software project using some good practices from the start. 
This will lay the foundation for long-term sustainability of our code, collaboration, and reproducibility. 

This starts with following naming conventions for files, employing version control, and (in the next episode) 
setting up a virtual development environment with software dependencies to ensure the project can be more easily and 
reliably run, shared and maintained. Next (over the rest of the course) - adding tests, setting up automation (e.g. continuous integration), 
documenting software and including metadata such as licensing, authorship and citation will ensure the results our software 
produces can be trusted and others can build upon it with confidence.

Let's begin by creating a new software project from our existing code,
and start tracking changes to it with version control.

## From script to software project

In the previous episode you have unzipped `spacewalks.zip` into a directory `spacewalks` in your home directory.
If you have not opened the software directory in VS Code already – go to **File -> Open Folder** and find `spacewalks`.

We also need access to a command line terminal to type various commands. In VS Code start a new terminal 
via **Terminal -> New Terminal** (Windows users need to make sure the new terminal is "GitBash"; not "PowerShell" or "cmd"). 
Alternatively, you can work with a shell terminal directly (and not within VS Code), if you so prefer.

If you are not already inside this directory, from your command line terminal you can navigate to it and list its 
contents with:

```bash
cd ~/spacewalks
ls -la
total 288
drwx------@  6 mbassan2  staff     192 30 Jul 10:56 .
drwxr-x---+ 55 mbassan2  staff    1760 14 Nov 14:34 ..
-rw-r--r--@  1 mbassan2  staff    6148 30 Jul 10:54 .DS_Store
drwxrwxr-x@  4 mbassan2  staff     128  4 Apr  2025 astronaut-data-analysis-old
-rw-rw-r--@  1 mbassan2  staff  132981  4 Apr  2025 data.json
-rw-rw-r--@  1 mbassan2  staff    1514 30 Jul 10:56 my code v2.py
```

Over the rest of the course, we will transform a collection of these files into a well-structured software project that 
follows established good practices in research software engineering.

The first thing you may notice that our software project contains folder `astronaut-data-analysis-old` which presumably tries to keep track
of older versions of the code. There is a better way to do that using version control tool, such as Git, and we can delete this folder so it does not cause confusion.

```bash
rm -r astronaut-data-analysis-old
```

## Version control

Before we do any further changes to our software, we want to make sure we can keep a history of what changes we have done since 
we inherited the code from our colleague.

We can track changes with a version control system (we will use Git). 
Later on, we will store those changes on a remote server too -- both for safe-keeping and to make them easier to share with others. 
In later episodes, we will also see how version control makes it easier for multiple collaborators to work together on the same project at the same time and combine their contributions.

:::::: callout

### Version control refresher

#### What is a version control system?

Version control systems are tools that let you track changes in files over time in a special database that allows 
users to "travel through time", and compare earlier versions of the files with the current state.
Think of a version control system like turning on 'Track Changes' on Microsoft Word/Google Docs,
but for *any* files you want, and a lot more powerful and flexible.

#### Why use a version control system?

As scientists, our main motivation for using version control is **reproducibility**.
By tracking and storing every change we make,
we can restore our project to the state it was at any point in time.
This is incredibly useful for reproducing results from a specific version of the code,
or tracking down which changes we (or others) made introduced bugs or changed our results.

The other benefit of version control is it provides us with a **history** of our development.
As we make each change, we record what it was, and why we made it.
This helps make our development process transparent and auditable -- which is a good scientific practice.

It also makes our project more **sustainable** - as our data, software and methods (knowledge) remain usable and
accessible over time (especially if made available in shared version controlled code repositories), even after the original funding ends or team members move on.

::::::

### Git version control system

**Git** is the most popular version control system used by researchers worldwide, and the one we'll be using.
Git is used mostly for managing code when developing software, but it can track *any* files --
and is particularly effective with text-based files (e.g. source code like `.py`, `.c`, `.r`, but also `.csv`, `.yml`, `.json` and more).

Git helps multiple people work on the same project (even the same file) at the same time.
Initially, we will use Git to start tracking changes to files on our local machines; later on we will start sharing our
work on GitHub allowing other people to see and contribute to our work.

:::::: callout

### Git refresher

Git stores files in **repositories** - directories where changes to the files can be tracked.
The diagram below shows the different parts of a Git repository,
and the most common commands used to work with one.

![Software development lifecycle with Git](fig/ep02_fig05-git-lifecycle.svg){alt='Software development lifecycle with Git diagram showing Git commands and flow of data between components of a Git system, including working directory, staging area, local and remote repository'}

- **Working directory** - a local directory (including any subdirectories) where your project files live,
  and where you are currently working.
  It is also known as the “untracked” area of Git.
  Any changes to files will be marked by Git in the working directory.
  Git will only *save* changes that you explicitly tell it to.
  Using `git add FILENAME` command, can you tell Git to start tracking changes to file `FILENAME` in your working directory.
- **Staging area (index)** - once you tell Git to start tracking changes to files (with `git add FILENAME` command),
  Git saves those changes in the staging area on your local machine.
  Each subsequent change to the same file needs to be followed by another `git add FILENAME` command to tell Git to update it in the staging area.
  To see what is in your working directory and staging area at any moment (i.e. what changes is Git tracking),
  you can run the command `git status`.
  The staging area lets you bundle together groups of changes to save to your repository.
- **Local repository** - stored within the `.git` directory of your project locally,
  this is where Git wraps together all your changes from the staging area and puts them using the `git commit` command.
  Each commit is a new, permanent snapshot (checkpoint, record) of your project in time, which you can share or revert to.
- **Remote repository** - this is a version of your project that is hosted somewhere on the Internet (e.g., on GitHub, GitLab or somewhere else).
  While your project is nicely version-controlled in your local repository,
  and you have snapshots of its versions from the past,
  if your machine crashes you still may lose all your work.
  Plus, sharing or collaborating on local work with others requires lots of emailing back and forth.
  Working with a remote repository involves 'pushing' your local changes to it (using `git push`),
  and pulling other people’s changes back to your local copy (using `git fetch` or `git pull`).
  This keeps the two in sync in order to collaborate, with a bonus that your work also gets backed up to another machine.
  Best practice when collaborating with others on a shared repository is to always do a `git pull` before a `git push`,
  to ensure you have any latest changes before you push your own.

::::::

### Start tracking changes with Git

Open up VS Code and launch a terminal.
By default, it will locate you in your `spacewalks` directory.
We want to tell Git to make `spacewalks` a repository -- a directory where Git can track changes to our files. 
We can do that with the `git init` command:

```bash
$ git init
```

We can check everything is set up correctly by asking Git to tell us the status of our project:

```bash
$ git status
```

```output
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.DS_Store
	data.json
	my code v2.py

nothing added to commit but untracked files present (use "git add" to track)
```

This tells us that Git has noticed three files in our directory, but unlike Dropbox or OneDrive, it does not *automatically* track them. 
We need to tell Git explicitly which files we want it to track.
This is not a handicap, but rather helpful, since software projects can have vast input or output files we might not want Git to track and store (e.g. think of GBs to TBs of space telescope data) or require sensitive information we cannot share (for example, medical records).
Or indeed contain hidden files that have nothing to do with the software project itself (e.g. `.DS_Store`) that we do not want to track or share.

Let's still commit our files (even though we know the code is broken) - we will note that the code is broken in our commit message.
This is a best practice if you decide to commit broken code.

### Adding files to a repository

We can tell Git to track a file using `git add`:

```bash
$ git add my\ code\ v2.py
$ git add data.json
```
and then check the right thing happened:

```bash
$ git status
```

```output
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   data.json
	new file:   my code v2.py

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.DS_Store
```

Git now knows that should track the changes to `my code v2.py` and `data.json`, but it has not 'committed' those changes to the record yet.
A commit is a snapshot of how your tracked files have changed at a stage in time.
To create a commit that records we added two new files, we need to run one more command:

```bash
$ git commit -m "Add the initial spacewalks data and code

BREAKING CHANGE: Path to data is hard coded and needs to be fixed"
```

```output
[main (root-commit) bf55eb7] Add the initial spacewalks data and code
 2 files changed, 437 insertions(+)
 create mode 100644 data.json
 create mode 100644 my code v2.py
```

The `-m` option means message, and records a short, descriptive, and specific comment that will help us remember later on what we did and why.
If we run `git commit` *without* `-m`, Git will still expect a message and and will launch a text editor so that we can write a longer one.

Remember, good commit messages start with a brief (<50 characters) statement about the changes made in the commit.
Generally, the message should complete the sentence "If applied, this commit will...".
If you want to go into more detail, add a blank line between the summary line and your additional notes.
Use this additional space to explain why you made changes and/or what their impact will be.

::::::::::::::::::::::::::::::::::::::::::::::::: instructor

### Choose how you teach version control steps from here

At this point in the lesson, you may choose to demonstrate how the same steps of staging and committing changes can also be achieved with the VS Code graphical interface.

![The Source Control interface to Git in VS Code](fig/vscode-source-control.png){alt="Screenshot of VS Code with the SOURCE CONTROL interface open in the left hand pane of the window. The interface shows one modified file staged for commit, an empty text input box where a commit message can be entered, and a green button labeled 'Commit & Push'"}

Depending on your relative levels of comfort working with that graphical interface and the command line interface to Git, you can choose how you want to demonstrate the remaining steps in this episode and when we use Git again elsewhere.
The lesson will continue to present version control steps with the command line interface only.

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

If we run `git status` now, we see:

```bash
$ git status
```

```output
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.DS_Store

nothing added to commit but untracked files present (use "git add" to track)
```

This tells us that everything is up to date.

At this point, Git has taken everything we have told it to save with the `git add` command and stored a copy (snapshot) of the files in a special, hidden `.git` directory.
This is called a commit (or revision).
You can check the existence of this special directory in VS Code's File Explorer.

:::::::::::::::::::::::::::::::::::::::::  callout

## Where are my changes?

If we run `ls` at this point, we'll still only see two files -- our script and our dataset.
Git saves information about our files' history in the special `.git` directory mentioned earlier.
This both stops our folders being cluttered with old versions, and *also* stops us accidentally deleting them!

You can see the hidden Git directory using the `-a` flag to show all files and folders:

```bash
$ ls -a
```

```output
.
..
.git
```

If you delete it, your directory will stop being a repository, and it will lose your history of changes.
You never need to look into or modify `.git` yourself -- Git has useful commands to do that, which are covered later on.

::::::::::::::::::::::::::::::::::::::::::::::::::

### Make a change

You may have noticed that the script we received contain blank spaces in filename.
This meant that, when we were typing the script's name into the terminal, we had to add a slash before the space like this: `my\ code\ v2.py`.
Using a backslash in this way is called "escaping".
It lets the terminal know to treat the space as part of the filename,
and not a separate argument.
It is a bit inconvenient and can cause problems if you forget,
so best practise is to avoid spaces in filenames.
The simplest fix is to replace the spaces with underscores `_` instead.

To rename the files using git you can use the `git mv` command:

```bash
$ git mv my\ code\ v2.py my_code_v2.py
```

If you run `git status` again, you'll see Git has noticed the change in the filename.
Note, `git mv` handles the name change directly, instead of seeing a deleted file and a new file as would be the case if we'd used `mv` and then `git add`.
It also stages the changes to be committed.

```bash
$ git status
```

```output
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	renamed:    my code v2.py -> my_code_v2.py

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.DS_Store
```

```bash
$ git commit -m "Remove spaces from filename"
```

### Rename our data and output files

Now that we know how to rename files in Git, we can use it to make our files and code a bit easier to understand.

We may want to:

1. Give our script and input data file more meaningful names, e.g. `eva_data_analysis.py` and `eva-data.json`. This change also uses removes version tracking from the script name as we are using Git for version control
any more as Git will keep track of that for us.
2. Choose informative file names for our output data file (e.g. `eva-data.csv`) and plot (`cumulative_eva_graph.png`).
3. Use relative paths (e.g. `./eva-data.json`) instead of absolute paths (e.g. `home/sarah/Projects/astronaut-analysis/data.csv`) to the files (which were hardcoded to the path on our colleagues machine and would not work on ours).
4. Update the Python script with these changes.

:::::::::::::::::::::::::::: challenge

#### Update the filenames (5 min)

Try to make these changes yourself.

1. Give our Python script and input data file informative names - `eva_data_analysis.py` and `eva-data.json`, respectively.
2. Update other file names and paths used in the script - output CSV data (`eva-data.csv` to match the new input data name) and plot(`cumulative_eva_graph.png`).
3. Stage and commit these changes in the Git repository.

:::::::::::::: solution

Firstly, let's update the file names in our Python script from VS Code:

```python
data_f = open('./eva-data.json', 'r')
data_t = open('./eva-data.csv','w')
g_file = './cumulative_eva_graph.png'
```

Next, we need to rename the files on the file system using Git:

```bash
git mv data.json eva-data.json
git mv my_code_v2.py eva_data_analysis.py
git add eva_data_analysis.py
git status
```
```output
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    data.json -> eva-data.json
        renamed:    my_code_v2.py -> eva_data_analysis.py

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .DS_Store
```

Finally, we can commit our changes:
```bash
git commit -m "Implement informative file names"
```

:::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::

Let's try to run our code again, see where we get to.

```bash
$ python3 eva_data_analysis.py
```

At this point you may get the following error if you do not have `matplotlib` installed on your system.

```bash
{'eva': '370', 'country': 'Russia', 'crew': 'Fyodor Yurchikhin;Alexander Misurkin;', 'vehicle': 'ISS Incr-36', 'date': '2013-08-16T00:00:00.000', 'duration': '7:29', 'purpose': 'Â\x95 Installed VINOSLIVOST experiment on MRM2, 2 MLMÂ\x96USOS power cables, FGB Â\x96 MRM2 gap spanners, MLM-USOS ETHERNET cable\nÂ\x95 Installation of gap spanners SM Â\x96 MRM2 (if time allows)\nÂ\x95 Retracted & stowed Strela-1 on DC1'}
1900-01-01 07:29:00 7.483333333333333
Traceback (most recent call last):
  File "/Users/user/spacewalks/eva_data_analysis.py", line 54, in <module>
    import matplotlib.pyplot as plt
ModuleNotFoundError: No module named 'matplotlib'
```

If you did not get the above error - you should now have the result graph file `cumulative_eva_graph.png` in your project root.
Note that we do not know if the plotted result file is correct or not.
You should also have the `eva-data.csv` file which contains the EVA data converted from JSON to CSV format.

We will look into the `matplotlib` issue in a moment.
But let's first set up our software project as a repository on GitHub so we can back up our work and share with others.

## Interacting with a remote Git server

Git is distributed version control system and lets us synchronise work between multiple copies of the same repository - 
which may not be on your machine (called **remote repositories**).
So far, we have used a **local repository** on our machine and,
even though we have been incrementally saving our work in a way that is recoverable,
if we lost our machine then we would lose all our code along with it,

Fortunately, we can easily upload our **local repository**, with all our code and the history of our development,
to a remote server so that it can be backed-up and recovered in future.

![Git - distributed version control system, image from W3Docs (freely available)](fig/git-distributed.png){alt='Two developers can use Git in combination with a remote repository, usually accessed via the internet. By pushing and pulling changes to and from the remote repository, they are each able to synchronise their local copy of the project with the changes the other developer has committed.'}

[GitHub][github] is an online software development platform that can act as a central remote server.
It uses Git, and provides facilities for storing, tracking, and collaborating on software projects.
Other Git hosting services are available, such as [GitLab](https://gitlab.com) and [Bitbucket](https://bitbucket.org).

Putting our projects on GitHub helps protect them against deletion,
and also makes it easy to collaborate and share them.
Our collaborators can access the project, download their own copy, and even contribute work back to us.

Let's push our **local repository** to [GitHub](https://github.com) and share it publicly.

1. In your browser, navigate to <https://github.com> and sign into your account.
2. In the top right hand corner of the screen,
   there is a menu labelled "+" with a dropdown.
   Click the dropdown and select "New repository" from the options:

   ![*Creating a new GitHub repository*](fig/ep02_fig01-create_new_repo.png){alt="Selecting the 'New repository' option from GitHub's dropdown menu labelled '+'" .image-with-shadow }

3. You will be presented with some options to fill in or select while creating your repository.
   In the "Repository Name" field, type "spacewalks".
   This is the name of your project and matches the name of your local folder.

   ![*Naming the GitHub repository*](fig/ep02_fig02-repository_name.png){alt="Setting the name of the repository on GitHub through the 'Repository Name' text field" .image-with-shadow }

   Ensure the visibility of the repository is "Public" and leave all other options blank.
   Since this repository will be connected to a local repository,
   it needs to be empty which is why we chose not to initialise with a README or add a license or `.gitignore` file.
   Click "Create repository" at the bottom of the page:

   ![*Complete GitHub repository creation*](fig/ep02_fig03-create_repository.png){alt="Completing the creation of the GitHub repository by clicking on the 'Create repository' button" .image-with-shadow }

4. Now we have a  **remote repository** on GitHub's servers,
   you need to send it the files and history from your **local repository**.
   GitHub provides some instructions on how to do that for different scenarios.
   Change the toggle on the right side from "HTTPS" to "SSH",
   then look at the heading "...or push an existing repository from the command line".
   You should see instructions that look like this:

   ```bash
   git remote add origin git@github.com/<YOUR_GITHUB_HANDLE>/spacewalks.git
   git branch -M main
   git push -u origin main
   ```

   **It is very important you make sure you switch from "HTTPS" to "SSH".**
   In the setup, we configured our GitHub account and our local machine for SSH.
   If you select HTTPS, you will not be able to upload your files.

   You can copy these commands using the button that looks like two overlapping squares to the right-hand side of the commands.
   Paste them into your terminal and run them.

  ![*Copy the commands to sync the local and remote repositories*](fig/ep02_fig04-copy_commands.png){alt="Copying the commands to sync the local and remote repositories from the remote repository's home page on GitHub" .image-with-shadow }

5. If you refresh your browser window,
   you should now see the two files `eva_data_analysis.py` and `eva-data.json` visible in the GitHub repository,
   matching what you have locally on your machine.

If you were wondering about what those commands did, here is the explanation.

```bash
git remote add origin git@github.com/<YOUR_GITHUB_HANDLE>/spacewalks.git
```

This command tells Git to create a `remote` called "origin" and link it to the URL of your GitHub repository.
A `remote` is a version control concept where two (or more) repositories are connected to each other,
in such a way that they can be kept in sync by exchanging commits.
"origin" is a name used to refer to the remote repository.
It could be called anything,
but "origin" is a common convention for Git since it shows which is considered the "source of truth".
This is particularly useful when many people are collaborating on the same repository.

```bash
git branch -M main
```

`git branch` is a command used to manage branches.
We'll discuss branches later on in the course.
We saw this command during setup and earlier in this episode - it ensures the branch we are working on is called "main".
This will be the default branch of the project for everyone working on it.

```bash
git push -u origin main
```

The `git push` command is used to update a remote repository with changes from your local repository.
This command tells Git to update the "main" branch on the "origin" remote.
The `-u` flag (short for `--set-upstream`) sets the 'tracking reference' for the current branch,
so that in future `git push` will default to sending to `origin main`.

## Software project in GitHub

We now have our software project in GitHub and have linked it to our local working copy.
We are ready to start more work on software development and publishing and backing up that work on GitHub.
Let's briefly explore the GitHub interface to our project.

![*GitHub repository interface*](fig/github-project-main-tabs.png){alt="Home page of a GitHub repository showing all the top-level tabs, including Code, Issues, Pull requests, Actions, projects, Wiki, Insights and Settings" .image-with-shadow }

In a GitHub software project, the tabs you see at the top of a repository page help organise different aspects of the project. 
Here's a brief explanation of them:

- **Code** - shows the source code, folders, and files in the repository. This is where the main development work is done.
- **Issues** - used to track bugs, tasks, feature requests, or any work that needs to be done.
- **Pull requests** - where contributors submit changes to the code. These are reviewed and discussed before being merged.
- **Actions** - automated workflows (like tests or deployments) that run on the project using GitHub Actions.
- **Projects** - offers a Kanban-style board to manage tasks and plan work (e.g., using cards and columns).
- **Wiki** – lets you create structured documentation for your project.
- **Security** – helps identify, manage, and fix vulnerabilities in your code and dependencies.
- **Insights** – provides analytics on project activity, contributions, and community health.
- **Settings** - where you configure how the repository behaves and how others can interact with it.

These tabs help manage collaboration, development, and maintenance of the project.
We will cover some of them in more detail as part of this course.
You may not see all of these tabs depending on your access level to the repository and the configuration settings. 

### Keeping track of issues and planned work in GitHub

The one tab that we want to start using early on is **Issues**. 
This is where you report issues and bugs, track tasks, feature requests and what needs to be done and what problems exist, and capture general discussions related to the project. 

Each issue acts like a conversation thread, where contributors can describe a problem or idea, discuss it, attach code snippets or images, and reference commits or pull requests or mention other team members.
It allows contributors to discuss and refine ideas before making changes, and helps prioritise work and organise releases.
The Issues tab serves as the project’s task board and communication hub, making development more organised, transparent and inclusive.

It is important to start listing things that need doing on the project early on so you do not forget about them. 
The Issues tab is a good place to create that list and keep it together with the code.

In one of the the previous exercises, we have identified a number of things that could be improved with our software. 
Let's add one of them as an issue now (we will continue to do this throughout the course - this is good practice).

For example, we identified that variables (e.g. `w`, `t`, `tt`, `ttt`) should have more descriptive and meaningful names.
To add this as an issue in GitHub, go to the **Issues** tab in your project's GitHub page, and click the "New issue" green button.
In the form that appears, we add a descriptive title for this new issue (e.g. "improve variable names") and write more details about the issue (e.g. "rename variables `w`, `t`, `tt`, and `ttt` to be more descriptive").

![*Adding an issue in GitHub*](fig/github-add-issue.png){alt="Form for adding an issue on a GitHub repository showing issue title and issue description fields" .image-with-shadow }

Later on in the course, we will learn how to comment, reference, add more details and close issues.

## Summary

We have created a new software project and used version control system Git to track changes to it. 
We can now look back at our work, compare different code versions, and even recover past states.
We have also published our software to a remote repository located on GitHub, where it is both secure and shareable.

These skills are critical to reproducible and sustainable science.
Software *is* science, and being able to share the specific version of code used in a paper is required for reproducibility.
But we, as researchers, also benefit from having a clear, self-documented record of what we did, when and why.
It makes it much easier to track down and fix our bugs, return to work on projects we took a break from,
and even for other people to pick up our work.

Before we start making changes to the code, we have to set up a development environment with software dependencies 
for our project to ensure this metadata about our project is recorded and shared with anyone wishing to download, run or extend our 
software (and this includes ourselves on a different machine or operating system).

:::::: spoiler

### Code state

At this point, the code in your local software project's directory should be as in:
<https://github.com/carpentries-incubator/bbrs-software-project/tree/03-reproducible-dev-environment>

:::

## Further reading

We recommend the following resources for some additional reading on the topic of this episode:

- [Software Carpentry's Git Novice lesson][swc-git-lesson]
- [The Turing Way's "Guide to Version Control"][ttw-guide-version-control]
- ["How Git Works" course on Pluralsight][how-git-works]
- [How to Write a Good Commit Message][good-commit-message]
- [Git Commit Good Practice][git-commit-good-practice]

Also check the [full reference set](learners/reference.md#litref) for the course.

:::::::::::::::::::::::::::::::::::::::: keypoints

- Version control systems are software that tracks and manages changes to a project over time
- Using version control aids reproducibility since the exact state of the software that produced an output can be recovered
- A commit represents the smallest unit of change to a project
- Commit messages describe what each commit contains and should be descriptive
- GitHub is a hosting service for sharing and collaborating on software
- Using version control is one of the first steps to creating a software project from a bunch of scripts - by investing 
in these practices early, researchers can create software that supports their work more effectively and enables others to build upon it with confidence.

::::::::::::::::::::::::::::::::::::::::::::::::::
