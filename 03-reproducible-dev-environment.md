---
title: Reproducible software environments
teaching: 30
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions

- What are virtual environments in software development and why use them?
- How can we manage Python virtual coding environments and external (third-party) libraries on our machines?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Set up a Python virtual coding environment for a software project using `venv` and `pip`.

::::::::::::::::::::::::::::::::::::::::::::::::

So far we have created a local Git repository to track changes in our software project and pushed it to GitHub
to enable others to see and contribute to it. We now want to start developing the code further.

:::::: spoiler

### Code state

At this point, the code in your local software project's directory should be as in:
<https://github.com/carpentries-incubator/bbrs-software-project/tree/03-reproducible-dev-environment>

::::::

::: instructor

Some learners may encounter various issues when creating and managing virtual development environments or configuring the Python interpreter path, depending on their specific system setup.

To assist with troubleshooting during workshops, we have compiled a list of common issues that instructors have observed in the past.

- learners sometimes forget to activate the virtual environment - instructors should remind the learners about this at the start of each episode and also check for this during episodes, e.g. each time a new command line terminal window is started.
- adding a Python installation to the beginning of the environment variable PATH, causes it to override Python from the virtual environment - always check for this with `which python3` and `python3 --version`.
- some learners have other environment variables set that can influence the Python interpreter and modules being loaded and used - e.g. `PYTHONHOME` (changes the location of the standard Python libraries), `PYTHONPATH` (augments the default search path for Python module files) or `PYTHONSTARTUP` (points to a Python script that is run before starting Python interactive mode for various enhancements like preloading modules, setting colors, etc.). Make sure they are unset before activating the environment, e.g. with:

```bash
$ unset PYTHONHOME PYTHONPATH PYTHONSTARTUP
$ python3 -m venv ./venv_spacewalks
```

If you run into problems not mentioned here, please open an [issue in the lesson repository](https://github.com/carpentries-incubator/better-research-software/issues/) so we can track them and update the lesson material accordingly.

:::

## Software dependencies

If we have a look at our script, we may notice a few `import` lines such as: `import json`, `import csv`, 
`import datetime as dt` and `import matplotlib.pyplot as plt` throughout the code.
This means that our code depends on or requires several **libraries** to function - namely `json`, `csv`, `datetime` and `matplotlib`.

`json`, `csv`, `datetime` are **standard Python libraries** - this means that they come included in a Python distribution and they will be provided for you to import out of the box.
If you are using some much older Python distributions for any reason, they may not include these libraries out of the box and you may still need to install them manually.

Python applications also use external libraries that do not come as part of the standard Python distribution - such as `matplotlib` or `pandas`.
This means that you will have to use a **package manager** tool to install them on your system.
Applications will also sometimes need a specific version of an external library (e.g. because they were written to work with feature, class, or function that may have been updated in more recent versions), or a specific version of Python interpreter.
This means that each Python application you work with may require a different setup and a set of dependencies so it is useful to be able to keep these configurations separate to avoid confusion between projects.

The solution for this problem is to create a self-contained **virtual environment** per project, which contains a particular version of Python installation plus a number of additional external libraries.
This is also the reason why we did not want to solve the `ModuleNotFoundError: No module named 'matplotlib'` (in the case you had it) from the previous episode there and then as it would mean installing `matplotlib` system-wide (i.e. globally on your machine).
It is much better to install libraries in virtual environments only for projects that need them.

## What are virtual software environments?

So what exactly are virtual software environments, and why use them?

A Python virtual environment helps us create an **isolated working copy** of a software project
that uses a specific version of Python interpreter
together with specific versions of a number of external libraries
installed into that virtual environment.
Python virtual environments are implemented as
directories with a particular structure within software projects,
containing links to specified dependencies
allowing isolation from other software projects on your machine that may require
different versions of Python or external libraries.

It is recommended to create a separate virtual environment for each project.
Then you do not have to worry about changes to the environment of the current project you are working on
affecting other projects - you can use different Python versions and different versions of the same third party
dependency by different projects on your machine independently from one another.

We can visualise the use of virtual environments for different Python projects on the same machine as follows:

![Diagram to depict different Python environments containing different packages on the same machine](fig/virtual-env.png){alt='A single system might contain multiple virtual environments, each containing a different version of Python and the set of third-party libraries it needs (dependencies) e.g. NumPy, Pandas or Matplotlib. Each environment contains its own complete copy of the required version of each dependency.'}

Another big motivator for using virtual environments is that they make sharing your code with others much easier -
as we will see shortly you can record your virtual environment in a special file and share it with your collaborators
who can then recreate the same development environment on their machines.

You do not have to worry too much about specific versions of external libraries
that your project depends on most of the time.
Virtual environments also enable you to always use
the latest available version without specifying it explicitly.
They also enable you to use a specific older version of a package for your project, should you need to.

:::::::::::::::::::::: callout

## Truly reproducible environments are difficult to attain

Creating and managing isolated environments for each of your software projects and sharing descriptions of those environments alongside the relevant code is a great way to make your software and analyses much more reproducible.
However, "true" computational reproducibility is very difficult to achieve.
For example, the tools we will use in this lesson only track the dependencies of our software, remaining unanware of other aspects of the software's environment such as the operating system and hardware of the system it is running on.
These properties of the environment can influence the running of the software and the results it produces and should be accounted for if a workflow is to be truly reproducible.

Although there is more that we can do to maximise the reproducibility of our software/workflows, the steps described in this episode are an excellent place to start.
We should not let the difficulty of attaining "perfect" reproducibility prevent us from implementing "good enough" practices that make our lives easier and are _much_ better than doing nothing.

::::::::::::::::::::::::::::::

## Managing virtual environments

There are several command line tools used for managing Python virtual environments - we will use `venv`,
available by default from the standard `Python` distribution since `Python 3.3`.

Part of managing your (virtual) working environment involves
installing, updating and removing external packages on your system.
The Python package manager tool `pip` is most commonly used for this -
it interacts and obtains the packages from the central repository called
[Python Package Index (PyPI)](https://pypi.org/).

So, we will use `venv` and `pip` in combination to help us create and share our virtual development environments.

### Creating virtual environments

Creating a virtual environment with `venv` is done by executing the following command:

```bash
$ python3 -m venv /path/to/new/virtual/environment
```

where `/path/to/new/virtual/environment` is a path to a directory where you want to place it -
conventionally within your software project so they are co-located.
This will create the target directory for the virtual environment.

For our project let's create a virtual environment called "venv_spacewalks" from our project's root directory.

```bash
$ python3 -m venv venv_spacewalks
```

If you list the contents of the newly created directory "venv_spacewalks", on a Mac or Linux system
(slightly different on Windows as explained below) you should see something like:

```bash
$ ls -l venv_spacewalks
```

```output
total 8
drwxr-xr-x  12 alex  staff  384  5 Oct 11:47 bin
drwxr-xr-x   2 alex  staff   64  5 Oct 11:47 include
drwxr-xr-x   3 alex  staff   96  5 Oct 11:47 lib
-rw-r--r--   1 alex  staff   90  5 Oct 11:47 pyvenv.cfg
```

So, running the `python3 -m venv venv_spacewalks` command created the target directory called "venv_spacewalks" containing:

- `pyvenv.cfg` configuration file with a home key pointing to the Python installation from which the command was run,
- `bin` subdirectory (called `Scripts` on Windows) containing a symlink of the Python interpreter binary used to create the environment and the standard Python library,
- `lib/pythonX.Y/site-packages` subdirectory (called `Lib\site-packages` on Windows) to contain its own independent set of installed Python packages isolated from other projects, and
- various other configuration and supporting files and subdirectories.

Once you’ve created a virtual environment, you will need to activate it.

On Mac or Linux, it is done as:

```bash
$ source venv_spacewalks/bin/activate
(venv_spacewalks) $
```

On Windows, recall that we have `Scripts` directory instead of `bin` and activating a virtual environment is done as:

```bash
$ source venv_spacewalks/Scripts/activate
(venv_spacewalks) $
```

Activating the virtual environment will change your command line’s prompt to show what virtual environment you are currently using (indicated by its name in round brackets at the start of the prompt).
It will also modify the environment so that running Python will get you the particular version of Python configured in your virtual environment.

You can verify you are using your virtual environment's version of Python by checking the path using the command `which`:

```bash
(venv_spacewalks) $ which python3
```

:::::::::::::::::::::::::::::::::::::::::: caution

### Environment Variables

Some learners encounter problems at this stage, where system-level packages are still used by Python instead of the versions installed into the virtual environment.
Previous participants solved the problem by unsetting the `PYTHONHOME`, `PYTHONPATH` and `PYTHONSTARTUP` environment variables before creating the virtual environment for the project:

```bash
$ unset PYTHONHOME PYTHONPATH PYTHONSTARTUP
$ python3 -m venv ./venv_spacewalks
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

### Naming Virtual Environments

What is a good name to use for a virtual environment?

Using `venv` or `.venv` as the name for an environment and storing it within the project's directory seems to be the standard practice - this way when you come across such a subdirectory within a software project, by convention you know it contains its virtual environment details.
A slight downside to this is that all different virtual environments on your machine will use the same name and the current one is determined by the context of the path you are currently located in.
Note that `.venv` is also a hidden directory and that may not be what you want to do.

We used `venv_spacewalks` - this deviates a from the convention of calling them `venv` or `.venv`, but does give a clear project-specific prompt of `(venv_spacewalks)` and indicates clearly it is a virtual environment.

Note that you can also set the command line prompt for the virtual environment:

```bash
python -m venv --prompt spacewalks venv
```
This will create a virtual environment in `venv` folder with `(spacewalks)` on the command line prompt.
It gives a shorter, meaningful prompt and sticks to convention at the same time.

In the future, you and your team decide what naming convention works best for you.

::::::::::::::::::::::::::::::::::::::::::::::::::

When you’re done working on your project, you can exit the environment with:

```bash
(venv_spacewalks) $ deactivate
```

If you've just done the `deactivate`, ensure you reactivate the environment ready for the next part:

```bash
$ source venv_spacewalks/bin/activate
(venv_spacewalks) $
```

Note that, since our software project is being tracked by Git, the newly created virtual environment will show up in version control - we will see how to handle it using Git in one of the subsequent episodes.

### Installing external packages

We noticed earlier that our code depends on four **external packages/libraries** -
`json`, `csv`, `datetime` and `matplotlib`.
As of Python 3.5, Python comes with in-built JSON and CSV libraries - this means there is no need to install these
additional packages (if you are using a fairly recent version of Python), but you still need to import them in any
script that uses them.
However, we still need to install packages such as `matplotlib` and `pandas` as they do not come as standard with Python distribution.

To install the latest version of `matplotlib` package with `pip` you use pip's `install` command and specify the package’s name, e.g.:

```bash
(venv_spacewalks) $ python3 -m pip install matplotlib
```

You can install multiple packages at once by listing them all, e.g.:

```bash
(venv_spacewalks) $ python3 -m pip install matplotlib pandas
```

The above command has installed package `matplotlib` in our currently active `venv_spacewalks` environment and will not affect any other Python projects we may have on our machines.

If you run the `python3 -m pip install` command on a package that is already installed, `pip` will notice this and do nothing.

To install a specific version of a Python package give the package name followed by `==` and the version number, e.g. `python3 -m pip install matplotlib==3.5.3`.

To specify a minimum version of a Python package, you can do `python3 -m pip install matplotlib>=3.5.1`.

To upgrade a package to the latest version, e.g. `python3 -m pip install --upgrade matplotlib`.

To display information about a particular installed package do:

```bash
(venv_spacewalks) $ python3 -m pip show matplotlib
```

```output
Name: matplotlib
Version: 3.9.0
Summary: Python plotting package
Home-page:
Author: John D. Hunter, Michael Droettboom
Author-email: Unknown <matplotlib-users@python.org>
License: License agreement for matplotlib versions 1.3.0 and later
=========================================================
...
Location: /opt/homebrew/lib/python3.11/site-packages
Requires: contourpy, cycler, fonttools, kiwisolver, numpy, packaging, pillow, pyparsing, python-dateutil
Required-by:
```

To list all packages installed with `pip` (in your current virtual environment):

```bash
(venv_spacewalks) $ python3 -m pip list
```

```output
Package         Version
--------------- -----------
contourpy       1.2.1
cycler          0.12.1
DateTime        5.5
fonttools       4.53.1
kiwisolver      1.4.5
matplotlib      3.9.2
numpy           2.0.1
packaging       24.1
pillow          10.4.0
pip             23.3.1
pyparsing       3.1.2
python-dateutil 2.9.0.post0
pytz            2024.1
setuptools      69.0.2
six             1.16.0
zope.interface  7.0.1
```

To uninstall a package installed in the virtual environment do: `python3 -m pip uninstall <package-name>`.
You can also supply a list of packages to uninstall at the same time.


:::::::::::::::::::::::::::::::::::::::::  callout

### Why not use `pip3 install <package-name>`?

You may have seen or used the `pip3 install <package-name>` command in the past, which is shorter and perhaps more intuitive than `python3 -m pip install <package-name>`. 

What is the difference?
`python3 -m pip install` uses Python to run the Pip module that comes with the Python distribution using the Python interpreter.
So `/usr/bin/python3.12 -m pip` means you are executing Pip for your Python interpreter located at `/usr/bin/python3.12`.

`pip3 install` runs the Pip module as an executable program with the same name - it may pick up whatever pip3 your PATH settings tell it to. 
And it may not be for the same Python version your expect - especially if you have several Python distributions (and Pips) installed (which is very common).
There are [edge cases](https://snarky.ca/why-you-should-use-python-m-pip/) when the two commands may produce different results, so be warned.

The [official Pip documentation](https://pip.pypa.io/en/stable/user_guide/#running-pip) recommends `python3 -m pip install` and that is what we will be using too.

::::::::::::::::::::::::::::::::::::::::::::::::::

### Sharing virtual environments

You are collaborating on a project with a team so, naturally,
you will want to share your environment with your collaborators
so they can easily 'clone' your software project with all of its dependencies
and everyone can replicate equivalent virtual environments on their machines.
`pip` has a handy way of exporting, saving and sharing virtual environments.

To export your active environment -
use `python3 -m pip freeze` command to produce a list of packages installed in the virtual environment.
A common convention is to put this list in a `requirements.txt` file in your project's root directory:

```bash
(venv_spacewalks) $ python3 -m pip freeze > requirements.txt
(venv_spacewalks) $ cat requirements.txt
```

```output
contourpy==1.2.1
cycler==0.12.1
DateTime==5.5
fonttools==4.53.1
kiwisolver==1.4.5
matplotlib==3.9.2
numpy==2.0.1
packaging==24.1
pillow==10.4.0
pyparsing==3.1.2
python-dateutil==2.9.0.post0
pytz==2024.1
six==1.16.0
zope.interface==7.0.1
```

The first of the above commands will create a `requirements.txt` file in your current directory.
Yours may look a little different, depending on the version of the packages you have installed, as well as any differences in the packages that they themselves use.

The `requirements.txt` file can then be committed to a version control system (we will see how to do this using Git in a moment) and get shipped as part of your software and shared with collaborators and/or users.

Note that you only need to share the small `requirements.txt` file with your collaborators - and not the entire `venv_spacewalks` directory with packages contained in your virtual environment.
We need to tell Git to ignore that directory, so it is not tracked and shared - we do this by creating a file `.gitignore` in the root directory of our project and adding a line `venv_spacewalks` to it.

```bash
(venv_spacewalks) $ echo "venv_spacewalks/" >> .gitignore
```
Remember the `.DS_Store` hidden file which is also not necessary to share with our project?
We can tell Git to ignore it by adding it on a new line in `.gitignore` as pattern `**/.DS_Store` (so it will be ignored in any sub-folder of our project).
That way it can safely reside in local projects of macOS users and can be ignored by the rest.

Let's add and commit `.gitignore` to our repository (this file we do want to track and share).

```bash
(venv_spacewalks) $ git add .gitignore
(venv_spacewalks) $ git commit -m "Ignore venv folder and DS_Store file"
```

The same method can be applied to ignore various other files that you do not want Git to track.

Let's now put `requirements.txt` under version control too and share it along with our code.

```bash
(venv_spacewalks) $ git add requirements.txt
(venv_spacewalks) $ git commit -m "Initial commit of requirements.txt"
(venv_spacewalks) $ git push origin main
```

Your collaborators or users of your software can now download your software's source code and replicate the same
virtual software environment for running your code on their machines using `requirements.txt` to install all
the necessary depending packages.

To recreate a virtual environment from `requirements.txt`, from the project root one can do the following:

```bash
(venv_spacewalks) $ python3 -m pip install -r requirements.txt
```

:::::::::::::::::::::: callout

### Another challenge in (long-term) reproducibility

For people (including your future self) to be able to reproduce software environments described in this way, the listed dependencies need to remain available to download and possible to install on the user's system.
These are reasonably safe assumptions for widely-used, actively maintained tools on commonly-used operating systems in the short- to medium-term.
However, it becomes less likely that we will be able to recreate such environments as system architectures evolve over time and maintainers stop supporting older versions of software.
To achieve this kind of long-term reproducibility, you will need to explore options to provide the actual environment -- with dependencies already included -- alongside your software, e.g. via a [containerised environment](https://carpentries-incubator.github.io/docker-introduction/).

::::::::::::::::::::::::::::::

As your project grows - you may need to update your environment for a variety of reasons, e.g.:

- one of your project's dependencies has just released a new version (dependency version number update),
- you need an additional package for data analysis (adding a new dependency), or
- you have found a better package and no longer need the older package
(adding a new and removing an old dependency).

What you need to do in this case (apart from installing the new and removing the packages that are no longer needed
from your virtual environment) is update the contents of the `requirements.txt` file accordingly
by re-issuing `pip freeze` command and propagate the updated `requirements.txt` file to your collaborators
via your code sharing platform.

:::::::::::::::::::::: callout

### Environment management can be troublesome

Software environment management is a difficult thing to get right, which is one reason why [the Python community has come up with so many different ways of doing it over the years](https://xkcd.com/1987). 
(That webcomic is several years old at the time of writing and the Python environment management ecosystem has only become _more_ complicated since.)
Unfortunately, even if you try to follow good practices and keep your environments isolated it is possible -- perhaps even likely -- that you will face difficulties with installing and updating dependencies on your projects in the coming years.
Such issues are particularly likely to appear when you upgrade your computer hardware, operating system, and/or interpreter/compiler.
As before, this is not a reason to avoid managing your software environments altogether -- or to avoid upgrading your hardware, operating system, etc! 
If you have descriptions of your environments it will always be easier to reproduce them and keep working with your software than if you need to start from scratch.
Furthermore, your expertise will develop as you get more practice with managing your software environments, which will equip you well to troubleshoot problems if and when they arise.

::::::::::::::::::::::::::::::

## Running the code and reproducing results

We are now setup to run our code from the newly created virtual environment:

```bash
(venv_spacewalks) $ python3 eva_data_analysis.py
```

You should get a pop up window with a graph.
However, some (but not all) Windows users will not.
You might instead see an error like:

```bash
Traceback (most recent call last):
  File "C:\Users\Toaster\Desktop\spacewalks\eva_data_analysis.py", line 30, in <module>
    w.writerow(data[j].values())
  File "C:\Program Files\WindowsApps\PythonSoftwareFoundation.Python.3.12_3.12.2544.0_x64__qbz5n2kfra8p0\Lib\encodings\cp1252.py", line 19, in encode
    return codecs.charmap_encode(input,self.errors,encoding_table)[0]
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
UnicodeEncodeError: 'charmap' codec can't encode character '\x92' in position 101: character maps to <undefined>
(spacewalks) (spacewalks)
```

This is not what we were expecting!
The problem is _character encoding_.
'Standard' Latin characters are encoded using ASCII,
but the expanded Unicode character set covers many more.
In this case, the data contains Unicode characters that are represented in the ASCII input file with shortcuts (`Â` as `\u00c2` and `’` as `\u0092`).

When we read the file, Python converts those into the Unicode characters.
Then by default Windows tries to write out `eva-data.csv` using UTF-7.
This saves space compared to the standard UTF-8,
but it doesn't include all of the characters.
It automatically converts `\u0092` into the shorter `\x92`,
then discovers that doesn't exist in UTF-7.

The fact that different systems have different defaults,
which can change or even break your code's behaviour,
shows why it is so important to make our code's requirements explicit!

We can fix this by explicitly telling Python what encoding to use when reading and writing our files 
(and you should do this even if you have not had the encoding error when running the code - it is good practice 
and otherwise it may catch you the next time you run the code on a different platform):

```python
...
data_f = open('./eva-data.json', 'r', encoding='ascii')
data_t = open('./eva-data.csv','w', encoding='utf-8')
...
```

Remember to commit these latest changes.

```bash
(venv_spacewalks) $ git add eva_data_analysis.py
(venv_spacewalks) $ git commit -m "Specify data encoding"
(venv_spacewalks) $ git push origin main
```

Do not forget to commit any files that have been changed.

## Summary

We now have our code running in its own virtual environment.

Virtual development environments provide significant benefits for software development by allowing developers to isolate project dependencies and configurations, preventing conflicts between projects.
They support reproducibility, making it much easier to recreate the same setup across different machines or for other team members, which helps with collaboration and consistency.
They allow us to share or deploy our environment setup easily, often as a single configuration file.
They promote a "cleaner" way of working and avoid polluting the global system environment with project-specific tools and packages.

In the next episode we will inspect our software in more detail and see how we can improve it further.

:::::: spoiler

### Code state

At this point, the code in your local software project's directory should be as in:
<https://github.com/carpentries-incubator/bbrs-software-project/tree/04-code-readability>

::::::

## Further reading

We recommend the following resources for some additional reading on the topic of this episode:

- [Official Python Documentation: Virtual Environments and Packages](https://docs.python.org/3/tutorial/venv.html)

Also check the [full reference set](learners/reference.md#litref) for the course.

:::::: keypoints

- Virtual environments keep Python versions and dependencies required by different projects separate.
- A Python virtual environment is itself a directory structure.
- You can use `venv` to create and manage Python virtual environments, and `pip` to install and manage external dependencies your code relies on.
- By convention, you can save and export your Python virtual environment in `requirements.txt` file in your project's root
directory, which can then be shared with collaborators/users and used to replicate your virtual environment elsewhere.

::::::
