---
title: Open software management & collaboration
teaching: 60
exercises: 30
---

::::::::::::::::::::::::::::::::::::: objectives
After completing this episode, participants should be able to:

- Create a digital object identifier (DOI) for a software project and archive it on Zenodo.
- Track the work needed to be done on code (such as bugs and new features) using issues in GitHub.
- Use Git branches to work on code in parallel with other team members.
- Merge code changes from separate development branches into the main branch using pull requests.

::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::: questions 

- How do can we create unique identifiers for our code so others can cite it?
- How do we archive our code for future preservation?
- How do we track issues with code in GitHub?
- How can we ensure that multiple developers can work on the same files simultaneously?

::::::::::::::::::::::::::::::::::::::::::::::::

Sharing code openly promotes collaboration, transparency, and innovation by allowing others to review, use, and improve the code. 
It fosters knowledge exchange, accelerates scientific progress, and enhances the reproducibility of research. 
Additionally, open sharing encourages community contributions and can lead to better-maintained, more reliable software.

Adding a [license](../learners/licensing.md) and other metadata to our code (covered in the previous episode) are the first steps towards sharing the code publicly.
There are several other important steps to consider which we will cover here.

:::::: spoiler

### Code state

At this point, the code in your local software project's directory should be as in:
<https://github.com/carpentries-incubator/bbrs-software-project/tree/08-open-collaboration>

::::::

::: spoiler

### Activate your virtual environment
If it is not already active, make sure to activate your virtual environment from the root of
the software project directory:

```bash
$ source venv_spacewalks/bin/activate # Mac or Linux
$ source venv_spacewalks/Scripts/activate # Windows
(venv_spacewalks) $
```
:::

## Sharing code to encourage collaboration

### Making the code public

By default repositories created on GitHub are private and only their creator can see them.
This prevents sensitive information from being unintentionally made public.
In our case - we added an open source license to our repository and want to make sure people can actually access and use it. 

To make your repository public (if it is not public already):

1. Go to your repository on GitHub and click on the `Settings` link near the top right corner. 
2. Scroll down to the bottom of the page and the "Danger Zone" settings. 
3. Click on "Change Visibility" and you should see a message saying "Change to public". 
If it says "Change to private" then the repository is already public. 
4. You will then be asked to confirm that you indeed want to make the repository public and agree to the warning that the code will now be publicly visible. 
As a security measure, you will then have to put in your GitHub password.

### Transferring to an organisation

At the moment, our repository sits under an individual GitHub user account. 
This is fine for smaller projects where one person is the main contributor. 
However, larger or more complex projects are typically hosted under a dedicated GitHub organisation. 
A GitHub organisation can group multiple repositories, manage contributor access through GitHub teams, and keep all project-related work in one place.
You can create a GitHub organisation to centrally manage all repositories for a single organisation or a multi-institution project."

If we are a member of a GitHub organisation and have the appropriate permissions then we can transfer a repository from our personal namespace to the organisation's. 
This can be done with another option in the "Danger Zone" settings - the "Transfer ownership" button. 
Pressing this will then prompt us as to which organisation we want to transfer the repository to (if we have access to multiple GitHub organisations). 

### Getting an identifier and archiving code

Putting code on GitHub or GitLab (or any similar code hosting service) is good practice for code sharing, versioning and even code packaging, it is not enough for long-term software archiving. 
This is because these are commercial services - if they change their policies, remove repositories (e.g. for inactivity, or security reasons), or even shut down (which has happened to code sharing platforms in the past), your code could disappear.
Archival means long-term preservation independent of any one platform.

Several archival solutions for research software are emerging.
[Zenodo][zenodo] is a data archive run by CERN which allows anyone to upload data up to 50GB for free and receive a Digital Object Identifier (DOI).
Zenodo's definition of "data" is quite broad and can include code - so it also supports DOI-backed software archiving linked to publications, ensuring persistent citation and access.

DOIs provide globally unique, citable references for a data or a software artefact (both software as a whole and its different releases) that integrates with various academic and research systems. 
Archival of and unique identifiers for software are important as they aid reproducibility, proper citation, and long-term accessibility of software.

Let us now look into how we can archive a GitHub repository to Zenodo and get a DOI for our software project at the same time. 
Note that, instead of using the real Zenodo website, we will practice using [Zenodo Sandbox](https://sandbox.zenodo.org/).

::: callout

### Zenodo Sandbox
[Zenodo Sandbox](https://sandbox.zenodo.org/) is a testing environment for Zenodo, a repository for research outputs, allowing users to safely experiment with its features without affecting the live system.
It is a clone of Zenodo, created for testing purposes, that works exactly the same way as Zenodo you can use it for learning, training, experimenting, and preparing uploads without impacting the primary Zenodo repository until
you are ready to publish and release your code (or other research outputs) officially.
It will also not create real DOIs for a number of test repositories we use for this course and saturate the DOI space (remember that a DOI, once created, is meant to exist forever).
:::

::::::::::: instructor

#### Optional challenge: archive our GitHub repository to Zenodo (5 min)

You can choose to do the following as an exercise or by live coding based on what you think the learners would prefer.
You can copy the detailed instructions below to give them it as an exercise.

::::::::::::::::::::::

We can archive our GitHub repository to Zenodo (Sandbox) by doing the following:

 1. Go to the [Zenodo Sandbox login page](https://sandbox.zenodo.org/login) and choose to login with GitHub.
 2. Authorise Zenodo Sandbox to connect to GitHub. 
 3. Go to the [GitHub page](https://sandbox.zenodo.org/account/settings/github/) in your Zenodo Sandbox account. 
This can be found in the pull down menu with your user name in the top right corner of the screen.
 4. You will now have a list of all of your GitHub repositories. Next to each will be an "On" button. 
If you have created a new repository you might need to press the "Sync" button to update the list of repositories 
Zenodo Sandbox knows about.
 5. Press the "On" button for the repository you want to archive. If this was successful you will be told to refresh the page.
 6. The repository should now appear in the list of "Enabled" repositories at the top of the screen, but it does not yet have a DOI. 
To get one we have to make a "release" on GitHub. 
To do so, click on the repository and then press the green button to create a release. 
This will take you to GitHub's release page for your software repository where you will be asked to give a title and description of the release. 
You will also have to create a "tag" for your release - a way of having a friendly name for the version of some code in Git instead of using a long hash code. 
Often we will create a sequential version number for each release of the software and have the tag name match this, for example v1.0 or just 1.0.
 7. If we now refresh the Zenodo Sandbox page for this repository we will see that it has been assigned a DOI.

The DOI does not just link to GitHub, Zenodo will have taken a copy (a snapshot) of our repository at the point where we created the release. 
This means that even if we delete it from GitHub or even if GitHub were ever to go away or remove it, there will still be a copy of our software on Zenodo. 
Zenodo will allow people to download the entire repository (more accurately, its state at the time it was tagged for release) as a single `zip` file. 

Zenodo will have actually created two DOIs for you. 
One represents the identifier for your software as a whole and will always link to the latest (most recent) release if you make more releases. 
The other is specific to the release you made and will always point to that version. 
We can see both of these by clicking on the DOI link in the Zenodo page for the repository.

One of the things which is displayed on this page is a badge image that you can copy the link for and add to the README file in your GitHub repository so that people can find the Zenodo version of the repository. 
If you click on the DOI image in the "Details" section of the Zenodo page then you will be shown instructions for obtaining a link to the DOI badge in various formats including Markdown.
Here is the badge for this repository and the corresponding Markdown: 

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.11869450.svg){alt='styled button linking to the Zenodo entry for this lesson'}](https://doi.org/10.5281/zenodo.11869450)

```text
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.11869450.svg)](https://doi.org/10.5281/zenodo.11869450)
```

::: spoiler

## Problems with GitHub and Zenodo integration

The integration between GitHub and Zenodo does not interact well with some browsers' privacy features and extensions. 
Firefox can be particularly problematic with this and might open new tabs to login to GitHub and then give an error saying: 
`Your browser did something unexpected. Please try again. If the error continues, try disabling all browser extensions.`
If this happens try disabling the extra privacy features/extensions or using another browser such as Chrome.

:::

### Adding a DOI to the citation file

Now that we have our DOI it is good practice to include this information in our software's citation file.
Earlier we created a `CITATION.cff` file with information about how to cite our software.
A DOI can be added to the `CITATION.cff` file using the dedicated `doi` key or by including it as an entry in the `identifiers:` array. 
Both methods are valid according to the CFF specification.
We can also add the `version` field to `CITATION.cff`, which corresponds to the version number of the software related to the DOI we are adding.

::::::::::: instructor

#### Optional challenge: add a DOI and software version to the citation file (5 min)

You can choose to do the following as an exercise or by live coding based on what you think the learners would prefer.
You can copy the the detailed instructions below to give it as an exercise.

::::::::::::::::::::::

We can add a DOI to the file by creating an `identifiers` section that includes the variables of `doi` and `value` of the Zenodo URL as a bulleted entry.
Optionally, we can also add a `date-released` field indicating the date we released this software as a new variable.
Here is an updated version of our `CITATION.cff` from the previous episode with a version number, DOI and release date added.

```yaml
# This CITATION.cff file was generated with cffinit.
# Visit https://bit.ly/cffinit to generate yours today!

cff-version: 1.2.0
title: Spacewalks
message: >-
  If you use this software, please cite it using the
  metadata from this file.
type: software
authors:
  - given-names: Jaffa
    name-particle: Sarah
  - given-names: Aleksandra
    family-names: Nenadic
  - given-names: Kamilla
    family-names: Kopec-Harding
repository-code: >-
  https://github.com/YOUR-REPOSITORY-URL/spacewalks.git
abstract: >-
  A Python script to analyse NASA extravehicular activity
  data
keywords:
  - NASA
  - Extravehicular activity
version: 1.0.1
identifiers:
  - type: doi
    value: 10.5281/zenodo.1234
date-released: 2024-06-01
```

::: callout

### Going further with publishing code

We now have our code published online, licensed as open source, archived with Zenodo, accessible via a DOI and with a citation file to encourage people to cite it.
What else might we want to do in order to improve how findable, accessible or reusable it is?
One further step we could take is to publish the code with a peer reviewed journal. 
Some traditional journals will accept software submissions, although these are usually as a supplementary material for a paper. 
There also journals which specialise in research software such as the [Journal of Open Research Software](https://openresearchsoftware.metajnl.com/), [The Journal of Open Source Software](https://joss.theoj.org/) or [SoftwareX](https://www.sciencedirect.com/journal/softwarex). 
With these venues, the submission will be the software itself and not a paper, although a short abstract or description of the software is often required.
:::

## Working with collaborators

The strength of online collaboration platforms such as GitHub does not just lie in the ability to share code. 
They also allow us to track problems with that code, for multiple developers to work on it independently and bring their changes together and to review those changes before they are accepted.

### Tracking issues with code

As we discussed earlier, a key feature of GitHub (as opposed to Git itself) is the issue tracker. 
This provides us with a place to keep track of any problems or bugs in the code and to discuss them with other developers. 
Sometimes advanced users will also use issue trackers of public projects to report problems they are having 
(and sometimes this is understandably misused by users seeking help using documented features of the program). 

To practice making an issue, we will file a "feature request", where we describe new functionality that may improve the codebase.
Let's go ahead and create a new issue in our GitHub repository for a feature request to create a table of total EVA/spacewalk time for each astronaut.
We can find the issue tracker on the "Issues" tab in the top left of the GitHub page for the repository. 
Click on this and then click on the green "New Issue" button on the right hand side of the screen. 
We can then enter a title and description of our issue.

A feature request should include a short title, the key features of the new feature, and a more detailed description of the feature, e.g.:

  - Title: Add summary table of EVA time by astronaut
  - Description: A summary table split by astronaut would be helpful for individual level analysis.

<!--- SCREENSHOT NEEDED: of example feature request -->

After the issue is created it will be assigned a sequential ID number.


### Discussing an issue

Once the issue is created, further discussion can take place with additional comments. 
These can include code snippets and file attachments such as screenshots or logfiles.
We can also reference other issues (by writing a `#` symbol and the number of the other issue) or mention other collaborators (by writing `@` followed by their GitHub username) to draw their attention to our comment. 
This is sometimes used to identify related issues or if an issue is a duplicate.


### Working in parallel with Git branches

Next, we will learn how to suggest this change back to the repository.
So far, we've been working on our own making changes in main.
However, when we start to have collaborators, we may need to adopt a workflow such as [GitHub flow](https://docs.github.com/en/get-started/using-github/github-flow) that facilitates simultaneous editing on the project and quality control on the changes made.

Branching is a feature of Git that allows two or more parallel streams of work. 
Commits can be made to one branch without interfering with another. 
Branches are commonly used as a way for one developer to work on a new feature or a bug fix while other developers work on other features.
When those new features or bug fixes are complete, the branch will be merged back with the `main` (sometimes called the `master`) branch.

#### Creating a new branch

New Git branches are created with the `git branch` command. This should be followed by the name of the branch to create. 
It is common practice when the bug we are fixing or feature we are adding has a corresponding issue to name the branch after the issue number and name. 
For example, we might call the branch `02-sum-by-astro-feat` instead of something less descriptive like `feature-request` or `bugfix`. 

For example, the command:

```bash
(venv_spacewalks) $ git branch 02-sum-by-astro-feat
```

will create a new branch called `02-sum-by-astro-feat`. 
We can view the names of all the branches by running `git branch` with no parameters.
By default there should be one branch called `main` (formerly `master`) and our new `02-sum-by-astro-feat` branch.
The command will put `*` next to the currently active branch.

```bash
(venv_spacewalks) $ git branch
```

```output
  02-sum-by-astro-feat
* main
```

We can see that creating a new branch has not switched our working branch to that branch. To switch branches we can either
use the `git switch` or `git checkout` command followed by the branch name. For example:

```bash
(venv_spacewalks) $ git switch 02-sum-by-astro-feat
```

To create a branch and change to it in a single command we can use `git switch` with the `-c` option 
(or `git checkout` with the `-b` option). 
Note that `git switch` command is only available in more recent versions of Git.
For example (learners do not have to execute this command):

```bash
(venv_spacewalks) $ git switch -c 03-summarize-categorical-bug
```

#### Committing to a branch

Once we have switched to a branch any further commits that are made will go to that branch. 
When we run a `git commit` command we will see the name of the
branch we are committing to in the output of `git commit`.
Let's add the following function to our code to implement the requested feature.

Copy and paste this function to add it to your code

```python
def sum_duration_by_astronaut(df, output_csv):
    """
    Summarizes the duration data by each astronaut and saves resulting table to a CSV file

    Args: 
        df (pd.DataFrame): The input dataframe to be summarized
        output_csv (str): Path to save the output csv of the table generated

    
    Returns:
        sum_by_astro (pd.DataFrame): Data frame with a row for each astronaut and a summarized column 
    """
    subset = df.loc[:,['crew', 'duration']] # subset to work with only relevant columns
    subset = add_duration_hours_variable(subset) # need duration_hours for easier calcs
    subset = subset.drop('duration', axis=1) # dropping extra duration file as those don't calculate correctly
    subset = subset.groupby('crew').sum() 
    print(f'Saving to CSV file {output_csv}')
    subset.to_csv(output_csv) # writing new table to specified location
    return subset
```

Then add the following to your main function, after the `eva_data` variable is created

```python
dur_by_astro = sum_duration_by_astronaut(eva_data, dur_by_astro_csv)
```

And we will add this line in our code to run if main, before or after we define the `graph_file` variable.
```python
dur_by_astro_csv = 'results/duration_by_astronaut.csv'
```

Now, let's test run our script, to make sure we do not get any errors.
```bash
(venv_spacewalks) $ python3 eva_data_analysis.py
```

If we do:
```
venv_spacewalks) $ ls results
```
we can see the new result CSV file listed.

Let's add and commit the new version of the code to our `02-sum-by-astro-feat` branch.
First we will check that we are on the right branch using either `git branch` or `git status`.

### Closing an issue

Once an issue is solved then it can be closed. 
This can be done either by pressing the "Close" button in the GitHub web interface (as we did before) or by making a commit which includes the word "fixes", "fixed", "close", "closed" or "closes" followed by a # symbol and the issue number in the commit message.

```bash
(venv_spacewalks) $ git branch
(venv_spacewalks) $ git add eva_data_analysis.py
(venv_spacewalks) $ git commit -m "added duration by astronaut functionality, closes #2"
```

In the output of `git commit -m` the first part of the output line will show the name of the branch we just made the commit to.

```output
[02-sum-by-astro-feat 330a2b1] added duration by astronaut functionality, closes #2
```

If we now switch back to the `main` branch our new commit will no longer be there in the source file or the output of `git log`.

```bash
(venv_spacewalks) $ git switch main
```

And if we go back to the `02-sum-by-astro-feat` branch it will re-appear.

```bash
(venv_spacewalks) $ git switch 02-sum-by-astro-feat
```

If we want to push our changes to a remote such as GitHub we have to tell the `git push` command which branch to push to. If the branch doesn't exist on the remote (as it currently won't)
then it will be created. 

```bash
(venv_spacewalks) $ git push origin 02-sum-by-astro-feat
```

If we now refresh the GitHub webpage for this repository we should see the `02-sum-by-astro-feat` branch has appeared in the list of branches.


::: spoiler 

#### How to pull changes from a remote branch 
If we needed to pull changes from a branch on a remote 
(for example if we have made changes on another computer or via GitHub's web based editor), 
then we can specify a branch on a `git pull` command.

```bash
git pull origin 02-sum-by-astro-feat
```
::::::::::

:::: spoiler

#### Merging branches

If we are working alone, when we have completed working on a branch (for example adding a feature or fixing a bug) then we can merge our branch back into the main one (or any other branch). 
This is done with the `git merge` command.

This must be run on the *TARGET* branch of the merge, so we will have to use a `git switch` command to set this. 

```bash
(venv_spacewalks) $ git switch main
```

Now we are back on the main branch we can go ahead and merge the changes from the bugfix branch:

```bash
(venv_spacewalks) $ git merge 02-sum-by-astro-feat
```
::::::::::::

### Pull requests

On larger projects, with collaborators, we might include a code review process before changes are merged. 
A quality control step like this is especially important if the main branch of the project is being released as the public version of the software.
GitHub has a process for this that is called a **Pull Request**. 
Other Git services such as GitLab have different names for this; GitLab calls them **merge requests**.
Pull requests are situations where one developer requests that another merges code from a branch (or "pull" it from another copy of the repository). 
The person receiving the request then has the chance to review the code, write comments suggesting changes or even change the code themselves before merging it. 
It is also very common for automated checks of code to be run on a pull request to ensure the code is of good quality and is passing automated tests.

As a simple example of a pull request, we can now create a pull request for the changes we made on our `02-sum-by-astro-feat` branch and pushed to GitHub earlier on. 
The GitHub webpage for our repository will now be saying something like "02-sum-by-astro-feat had recent pushes `n` minutes ago - Compare & Pull request". 
Click on this button and create a new pull request. 

Give the pull request a title and write a brief description of it, then click the green "Create pull request" button. 
GitHub will then check if we can merge this pull request without any problems.  

There should be a green "Merge pull request" button, but if we click on the down arrow inside this button there are three options on how to handle this request:

1. Create a merge commit
2. Squash and merge
3. Rebase and merge

The default is option 1, which will keep all of the commits made on our branch intact. 
This can be useful for seeing the whole history of our work, but if we've done a lot of minor edits or attempts at creating the feature it can be excessive to have all of this history saved. 
This is where the second option comes in, this will place all of our changes from the branch into just a single commit, this might be much more obvious to other developers who will now see our feature addition as a single commit in the history. 
The third option merges the branch histories together in a different way that doesn't make merges as obvious, this can make the history easier to read but effectively rewrites the commit history and will change the commit hash IDs. 
Some projects that you contribute to might have their own rules about what kind of merge they will prefer. 
For the purposes of this exercise we'll stick with the default merge commit. 

Go ahead and click on "Merge pull request", then "Confirm merge". 
The changes will now be merged together. 
GitHub gives us the option to delete the branch we were working on, since its history is preserved in the main branch there is no reason to keep it.

:::::: callout

#### Using forks instead of branches

A fork is similar to a branch, but instead of it being part of the same repository it is a entirely new copy of the repository. 
Forks are commonly used by Github users who wish to work on a project that they are not a member of. 
Typically forking will copy the repository to our own namespace (e.g. `github.com/username/reponame` instead of `github.com/projectname/reponame`).

To create a fork on github use the "Fork" button to the right of the repository name. 
After we create our fork we can make some changes and these could even be on the main branch inside our forked repository. 
GitHub will track that a fork has been made displays a "Contribute" button to create a pull request back to the original repository. 
Using this we can request that the changes on our fork are incorporated by the upstream project.

::::::::

:::  challenge

### Practice with Issues and PRs (20 min)

We have a bug in our code!  If we look at the results in `results/duration_by_astronaut.csv`, the crew column has groups of crew and we wanted to calculate this per astronaut. 

1. Create an issue in GitHub to report this bug. A good issue description for a bug should include:

 - What the problem is, including any error messages that are displayed.
 - What version of the software it occurred with.
 - Any relevant information about the system running it, for example the operating system being used.
 - Versions of any dependent libraries.
 - How to reproduce it.
 - (Optionally) description of the expected behaviour, e.g. if there is not an error message but the user thinks the result or behaviour is not correct.
 
We might also reference the previous issue in the description, to provide even more context (e.g. "related to #N" where N is the number of the feature request issue).

2. Create a pull request fix the code. You can try to create the code yourself or copy the test code below.
    - Hint: Do not forget to make a new branch from the `main` branch, not your `02-sum-by-astro-feat` branch.
3. (Optionally) Have a partner review your pull request.
3. Merge your pull request
4. Switch your local computer back to the `main` branch and pull the latest changes from the remote/origin `main` branch.
5. (Bonus/optional) Delete your merged branches from your local computer and in GitHub.

:::::: spoiler

#### Updated function to copy-paste

```python
def sum_duration_by_astronaut(df, output_csv):
    """
    Summarize the duration data by each astronaut and saves resulting table to a CSV file

    Args: 
        df (pd.DataFrame): The input dataframe to be summarized
        output_csv (str): Path to save the output csv of the table generated

    
    Returns:
        sum_by_astro (pd.DataFrame): Data frame with a row for each astronaut and a summarized column 
    """
    subset = df.loc[:,['crew', 'duration']] # subset to work with only relevant columns
    subset.crew = subset.crew.str.split(';').apply(lambda x: [i for i in x if i.strip()]) # splitting the crew into individuals and removing blank string splits from ending ;
    subset = subset.explode('crew') # separating lists of crew into individual rows
    subset = add_duration_hours_variable(subset) # need duration_hours for easier calcs
    subset = subset.drop('duration', axis=1) # dropping extra duration file as those don't calculate correctly
    subset = subset.groupby('crew').sum() 
    print(f'Saving to CSV file {output_csv}')
    subset.to_csv(output_csv) # writing new table to specified location
    return subset
```

:::::


:::

::::::::: callout

#### Reopening an Issue

In practice, a report of incorrect implementation of a new feature might be made as a comment on the original feature request issue rather than via a new issue. 
The project maintainers might then reopen that issue until the correction is made. 
For the purposes of this workshop, we want you to get more practice by opening a separate issue.

::::::::::::::::::


## Summary

This episode emphasises the importance of collaboration in creating sustainable research software. 
It covers practices like using open version control repositories (e.g., GitHub), inviting contributions through issue templates, PR and code review processes, and establishing clear governance, licensing, and codes of conduct. 
The episode also highlights the ethos of open collaboration so that anyone can contribute and benefit from the project, reinforcing transparency, inclusivity, and community-driven development.

:::::: spoiler

### Code state

At this point, the code in your local software project's directory should be as in:
<https://github.com/carpentries-incubator/bbrs-software-project/tree/final>

::::::

## Further reading

We recommend the following resources for some additional reading on the topic of this episode:

- Licencing and citation episodes from the [Software Carpentry's Git Novice lesson][swc-git-lesson]
- Carpentries GitHub Skill ups for [instructors][git-skillup-instructors] and [maintainers][git-skillup-maintainers]
- [RSG Southampton Git lesson][git-soton] - [collaboration section][git-soton-collaboration]
- [Open source definition][osd-definition], by the [Open Source Initiative][osd]
- [What is free software?][free-software]

Also check the [full reference set](learners/reference.md#litref) for the course.

:::::::::::::::::::::::::::::::::::::::: keypoints

- Zenodo can be used to archive a GitHub repository and obtain a DOI for it.
- We include a CITATION file with our code to tell people how to cite it.
- GitHub can help us track bugs or issues with software.
- Git branches can be used to allow multiple developers to work on the same part of code in parallel.
- The `git branch` command shows the list of branches and can create new branches.
- The `git switch` command changes which branch we are working on.
- The `git merge` command merges another branch into the current one.
- Pull requests allow developers to work on their own branch/fork and then request other developers review 
their changes before they are merged.

::::::::::::::::::::::::::::::::::::::::::::::::::
