---
title: "Course introduction"
teaching: 10
exercises: 10
---

:::::::::::::::::::::::::::::::::::::: questions

- What is open and reproducible research?
- Why are these practices important, in particular in the context of software used to support such research?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Describe the principles of open and reproducible research and why they are of value in the research community
- Explain how the concept of reproducibility translates into practices for building better research software
- Setup machine with software and data used to teach this course

::::::::::::::::::::::::::::::::::::::::::::::::

Software is [fundamental to modern research][ssi-survey-2014] - some of it would even be impossible without software.
From short, thrown-together temporary scripts written to help with day-to-day research tasks, through an abundance of complex data analysis spreadsheets, to the hundreds of software engineers and millions of lines of code behind international efforts such as the Large Hadron Collider, there are few areas of research where software does not have a fundamental role.

This course teaches good practices and reproducible working methods that are agnostic of a programming language (although we will use Python code in our examples).
It aims to provide researchers with the tools and knowledge to feel confident when writing **good quality and sustainable software** to support their research.
Although the discussion will often focus on software developed in the context of research, most of the good practices introduced here are beneficial to software development more generally.

The lesson is particularly focused on one aspect of good (scientific) software development practice: improving software to enhance reproducibility.
That is, enabling others to run our code and obtain the same results we did.

:::::::::::::::::::::: callout

## Why should I care about reproducibility?

Scientific transparency and rigor are key factors in research.
Scientific methodology and results need to be published openly and replicated and confirmed by several independent parties.
However, research papers often lack the full details required for independent reproduction or replication. 
Many attempts at reproducing or replicating the results of scientific studies have failed in a variety of disciplines ranging from psychology ([The Open Science Collaboration (2015)][replication-crisis-osc]) to cancer sciences ([Errington et al (2021)][replication-crisis-errington]).
These are called [**the reproducibility and replicability crises**][reproducibility-crisis] - ongoing methodological crises in which the results of many scientific studies are difficult or impossible to repeat.

Reproducible research is a practice that ensures that researchers can repeat the same analysis multiple times with the same results.
It offers many benefits to those who practice it:

* Reproducible research helps researchers remember how and why they performed specific tasks and analyses; this enables easier explanation of work to collaborators and reviewers.
* Reproducible research enables researchers to quickly modify analyses and figures - this is often required at all stages of research and automating this process saves loads of time.
* Reproducible research enables reusability of previously conducted tasks so that new projects that require the same or similar tasks become much easier and efficient by reusing or reconfiguring previous work.
* Reproducible research supports researchers' career development by facilitating the reuse and citation of all research outputs - including both code and data.
* Reproducible research is a strong indicator of rigor, trustworthiness, and transparency in scientific research.
  This can increase the quality and speed of peer review, because reviewers can directly access the analytical process described in a manuscript.
  It increases the probability that errors are caught early on - by collaborators or during the peer-review process, helping alleviate the reproducibility crisis.  

However, reproducible research often requires that researchers implement new practices and learn new tools.
This course aims to teach some of these practices and tools pertaining to the use of software to conduct reproducible research.

Review [the Reproducible Research Discussion](./reproducible-research-discussion.md) for a more in-depth discussion of this topic.

::::::::::::::::::::::::::::::

## Practices for building better research software

The practices we will cover for building better research software fall into three areas.

### 1. Things you can do with your own computing environment to enhance the software

* Using virtual development environments ensures your software can be developed and run consistently across different systems, making it easier for you and others to run, reuse, and extend your code.

### 2. Things you can do to improve the source code of the software itself

* Organising and structuring your code and project directory keeps your software clean, modular, and reusable, enhancing its readability, extensibility, and reusability.
* Following coding conventions and guides for your programming language ensures that others find it easy to read your code, reuse or extend it in their own examples and applications.
* Testing can save time spent on debugging and ensures that your code is correct and does what it is set out to do, giving you and others confidence in your code and the results it produces.

### 3. Things you can do to make the software easier for other people to use

* Using version control and collaboration platforms like [GitHub](https://github.com), [GitLab](https://gitlab.com), and [CodeBerg](https://codeberg.org/) makes it easier to share code and work on it together.
* Fostering a community around your software and promoting collaboration helps to grow a user base for your software and contributes to its long-term sustainability.
* Providing clear and comprehensive documentation, including code comments, API specifications, setup guides, and usage instructions, ensures your software is easy to understand, use, and extend (by you and others).
* Accompanying your software with clear information about its licensing terms and how it should be cited ensures that others can reuse and adapt your code with confidence and that you receive credit when they do so.

:::::::::::::::::: challenge

### Tools and practices you use (10 min)

Individually,

- reflect on what practices or tools you are already using in your software development workflow,
- list some new practices or tools that you would like to start employing or using.

Write your reflections in the shared collaborative document.

::::::::::::::::::

## Our research software project

You are going to follow a fairly typical experience of a new researcher (e.g. a PhD student or a postdoc) joining a research group.
You were emailed some spacewalks data and analysis code bundled in the `spacewalks.zip` archive, written by another group 
member who worked on similar things but has since left. You need to be able to install and run this code on your 
machine, check you can understand it and then adapt it to your own project.

As part of the [setup for this course](./installation-instructions.html#spacewalks), you may have downloaded or been emailed the `spacewalks.zip` archive. 
If not, you can [download it](./installation-instructions.html#spacewalks) now.
Save the `spacewalks.zip` archive to your home directory and extract it - you should get a directory called `spacewalks`.

The first thing you may want to do is inspect the content of the code and data you received to learn more about what it does. 
We will use VS Code for browsing, inspecting, modifying files and running our code.

VS Code is a very handy tool for software development and is used by many researchers worldwide. 
It "understands" the syntax of many different file types - for example Python, JSON, CSV, etc. - 
either natively or via extensions that can be installed. To open our directory `spacewalks` in VS Code – go to **File -> Open Folder** and find `spacewalks`.

You may notice that the software project contains:

1. A JSON file called `data.json` - a snippet of which is shown below - with data on extra-vehicular activities 
(EVAs, i.e. spacewalks) undertaken by astronauts and cosmonauts from 1965 to 2013 (data provided by NASA via its [Open Data Portal](https://data.nasa.gov/Raw-Data/Extra-vehicular-Activity-EVA-US-and-Russia/9kcy-zwvn/about_data)).

   ![JSON data file snippet showing EVA/spacewalk data including EVA ID, country, crew members, vehicle type, date of the spacewalk, duration, and purpose](fig/astronaut-data-json-snippet.png){alt='JSON data file snippet showing EVA/spacewalk data including EVA ID, country, crew members, vehicle type, date of the spacewalk, duration, and purpose'}
2. A Python script called `my code v2.py` containing some analysis code.

   ![The first few lines of a Python script](fig/astronaut-analysis-bad-code-screenshot.png){alt='The first few lines of a Python script used as example code for the episode'}

   The code in the Python script does some common research tasks:

  * Reads in the data from the JSON file
  * Changes the data from one data format to another and saves to a file in the new format (CSV)
  * Performs some calculations to generate summary statistics about the data
  * Makes a plot to visualise the data

3. A folder called `astronaut-data-analysis-old` - which presumably contains previous versions of the analysis acting as some sort of a backup.
4. A hidden file `.DS_Store` - Desktop Services Store is a hidden metadata file automatically created by macOS Finder in every folder, storing user-specific view settings like icon positions, window size, and background colors, acting much like Windows' `desktop.ini`.
This makes us think that the author was using macOS operating system but this file does not make part of the project itself.

If you do not see hidden file `.DS_Store`, that means that your VS Code is configured to exclude certain files and directories from the File Explorer View.
One way to modify this is going to ‘Code’ > ‘Preferences’ > ‘Settings’ (‘Code’ > ‘Preferences’ > ‘Settings’ on macOS) and searching for ‘exclude’ and you will find the default exclude list under `Files: exclude`.
You can remove the `**/.DS_Store` pattern and the hidden file `.DS_Store` should appear in VS Code's File Explorer.

Alternatively, open a terminal window within VS Code, navigate to your `spacewalks` folder (we are assuming you downloaded it into your home directory) and issue `ls -la` command to list the directory contents.

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

:::::: challenge

### Assess the software project (15 min)

Individually inspect the code and data.
Try and see if you can understand what the code is doing and how it is organised.

In the shared document, write down anything that you think is not "quite right", not clear, is missing, or could be done better.

::: hint

Below are some suggested questions to help you assess the code.
These are not the only criteria on which you could evaluate the code and you may find other aspects to comment on.

- If these files were emailed to you, or sent on a chat platform, or handed to you on a memory stick, how easy would it be to find them again in 6 months, or 3 years?
- Can you understand the code? Does it make sense to you?
- Could you run the code on your platform/operating system (is there documentation that covers installation instructions)? What programs or libraries do you need to install to make it work (and which versions)? Are these commonly used tools in your field?
- Are you allowed to reuse this code in your own work? If you did, would the owner expect credit in some form (paper authorship, citation or acknowledgement)? Are you allowed to modify the files or share them with others?
- Is the code written in a way that allows you to easily modify or extend it? How easy would it be to change its parameters to calculate a different statistic, or run the analysis on a different input file?

:::

::: solution

### Solution

This is a (non-exhaustive) list of things that could be fixed/improved with our code and data:

#### File and variable naming

- data (`data.json`) and Python script (`my code v2.py`) files could have more descriptive names
- Python script (`my code v2.py`) should not contain blank spaces as it may cause problems when running the code from command line
- variables (e.g. `w`, `t`, `tt`, `ttt`) should have more descriptive and meaningful names
- version control is embedded in the file name (`my code v2.py`) - there are better ways of keeping track of changes to code and its different versions
- the project contains a hidden file `.DS_Store` which is local and personal config file that should not be shared and does not even make sense other than on macOS

#### Code organisation and style

- import statements should be grouped at the top
- commenting and uncommenting code should not be used to direct the flow of execution / type of analysis being done
- the code lacks comments, documentation and explanations
- code structure could be improved to be more modular and not one monolithic piece of code - e.g. use functions for reusable units of functionality
- unused variables (e.g. `fieldnames` meant to be used when saving data to CSV file) are polluting the code and confusing the person reading the code
- spaces should not be used in column names as it can lead to error when reading the data in

#### Code content and correctness

- fixing the loop to 374 data entries is not reusable on other data files and would likely break if the data file changed
- running the code twice causes the program to fail as the result file from the previous run will exist (which the code does not check for) and the script will refuse to overwrite it
- the code does not specify the encoding when reading the data in, and we are also not sure what encoding the data was saved in originally
- how can we be confident the data analysis and plot that is produced as a result are correct?

#### Documentation

- there is no README documentation to orient the user
- there is no licence information to say how the code can be reused (which then means it cannot be reused at all)
- it is not clear what software dependencies the code has
- there are no installation instructions or instructions on how to run the code

:::

::::::

As you have seen from the previous exercise - there are quite a few things that can be improved with this code.
We will try to make this research software project a "bit better" for future use.

Let's check your setup now to make sure you are ready for the rest of this course.

::::::  challenge

### Check your setup (5 min)

From a command line terminal on your operating system or within VS Code run the following commands to check you have 
installed all the tools listed in [the Setup page](./installation-instructions.html) and that are functioning correctly.

Checking the command line terminal:

1. `$ date`
2. `$ echo $SHELL`
3. `$ pwd`
4. `$ whoami`

Checking Python:

5. `$ python --version`
6. `$ python3 --version`
7. `$ which python`
8. `$ which python3`

Checking Git and GitHub:

9. `$ git --help`
10. `$ git config --list`
11. `$ ssh -T git@github.com`

Checking VS Code:

12. `$ code`
13. `$ code --list-extensions`

::: solution

The expected out put of each command is:

1. Today's date
2. `bash` or `zsh` - this tells you what shell language you are using. In this course we show examples in Bash.
3. Your "present working directory" or the folder where your shell is running
4. Your username
5. In this course we are using Python 3. If `python --version` gives you Python 2.x you may have two versions of Python installed on your computer and need to be careful which one you are using.
6. Use this command to be certain you are using Python version 3, not 2, if you have both installed.
7. The file path to where the Python version you are calling is installed.
8. If you have more than one version these should be different paths, if both 5. and 6. gave the same result then 7. and 8. should match as well.
9. The help message explaining how to use the `git` command.
10. You should have `user.name`, `user.email` and `core.editor` set in your Git configuration. Check that the editor listed is one you know how to use.
11. This checks if you have set up your connection to GitHub correctly. If is says `permission denied` you may need to look at the instructions for setting up SSH keys again on the Setup page.
12. This should open VS Code in your current working directory. macOS users may need to first open VS Code and [add it to the PATH](https://code.visualstudio.com/docs/setup/mac#_launching-from-the-command-line).
13. If you installed the [VS Code extensions during setup](./installation-instructions#vs-code-extensions-for-python), you should see the extensions GitLens, Git Graph, Python, JSON and Excel Viewer in the output list.

:::

::::::

## Further reading

We recommend the following resources for some additional reading on reproducible research:

* [Reproducible research through reusable code][nesc-ttw-guide-reproducible-research] is a one day course by the [Netherlands eScience Center][nesc] which discusses similar themes to this course, but in a shorter format.
* [The Turing Way's "Guide for Reproducible Research"][ttw-guide-reproducible-research]
* [A Beginner's Guide to Conducting Reproducible Research][beginner-guide-reproducible-research], Jesse M. Alston, Jessica A. Rick, Bulletin of The Ecological Society of America 102 (2) (2021), https://doi.org/10.1002/bes2.1801
* ["Ten reproducible research things" tutorial][10-reproducible-research-things]
* [FORCE11's FAIR 4 Research Software (FAIR4RS) Working Group][fair4rs-working-group]
* ["Good Enough Practices in Scientific Computing" course][good-enough-practices]
* [Reproducibility for Everyone's (R4E) resources][repro4everyone], community-led education initiative to increase adoption of open research practices at scale
* [Training materials on different aspects of research software engineering][intersect-rse-training] (including open source, reproducibility, research software testing, engineering, design, continuous integration, collaboration, version control, packaging,  etc.), compiled by the [INTERSECT project](https://intersect-training.org/)
* [Curated resources][forrt-resources] by the [Framework for Open and Reproducible Research Training](https://forrt.org/) (FORRT)

## Acknowledgements and references

The content of this course borrows from or references [various work](learners/reference.md#litref).
