---
title: Continuous Integration for automated testing
teaching: 20
exercises: 20
---

:::::::::::::::::::::::::::::::::::::: questions

- How can I automate the testing of my repository's code in a way that scales well?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

After completing this episode, participants should be able to:

- Describe the benefits of using Continuous Integration for further automation of testing
- Enable GitHub Actions Continuous Integration for public open source repositories
- Use continuous integration to automatically run unit tests and code coverage when changes are committed to a version control repository

::::::::::::::::::::::::::::::::::::::::::::::::


This extra episode could be followed after the [episode on code correctness](../episodes/06-code-correctness.md) and with [the starter code from the end of that episode](https://github.com/carpentries-incubator/bbrs-software-project/tree/07-software-documentation).

::: callout

### Activate your virtual environment

If it is not already active, make sure to activate your virtual environment from the root of
the software project directory:

```bash
$ source venv_spacewalks/bin/activate # Mac or Linux
$ source venv_spacewalks/Scripts/activate # Windows
(venv_spacewalks) $
```
:::

So far in this course, we have run our tests locally from our software's root directory using, e.g.:

``` bash
$ python3 -m pytest
```

A limitation of this approach is that we must remember to run our tests
each time we make any changes. 
Continuous Integration (CI) services provide the infrastructure to
automatically run the test suite for our code every time changes are pushed to our remote code repository.
This means that each time we (or our colleagues) make a change, this will trigger the execution of the test suite
to verify that our tests still pass.

GitHub provides the Continuous Integration service called GitHub Actions for this purpose.

### How to Describe a Workflow?

Now before we move on to defining our workflow in GitHub Actions,
we'll take a very brief look at a language used to describe its workflows,
called YAML.

Originally, the acronym stood for *Yet Another Markup Language*,
but since it's not actually used for document markup,
it's acronym meaning was changed to *YAML Aint Markup Language*.

Essentially, YAML is based around key value pairs, for example:

```yaml
name: Kilimanjaro
height_metres: 5892
first_scaled_by: Hans Meyer
```

Now we can also define more complex data structures too.
Using YAML arrays, for example,
we could define more than one entry for `first_scaled_by`,
by replacing it with:

```yaml
first_scaled_by:
  - Hans Meyer
  - Ludwig Purtscheller
```

Note that similarly to languages like Python,
YAML uses spaces for indentation (2 spaces is recommended).
Also, in YAML, arrays are sequences,
where the order is preserved.

There's also a short form for arrays:

```yaml
first_scaled_by: [Hans Meyer, Ludwig Purtscheller]
```

We can also define nested, hierarchical structures too, using YAML *maps*.
For example:

```yaml
name: Kilimanjaro
height:
  value: 5892
  unit: metres
  measured:
    year: 2008
    by: Kilimanjaro 2008 Precise Height Measurement Expedition
```

We are also able to combine maps and arrays,
for example:

```yaml
first_scaled_by:
  - name: Hans Meyer
    date_of_birth: 22-03-1858
    nationality: German
  - name: Ludwig Purtscheller
    date_of_birth: 22-03-1858
    nationality: Austrian
```

So that's a very brief tour of YAML,
which demonstrates what we need to know to write GitHub Actions workflows.

### Defining our Workflow

Setting up GitHub Actions on our code repository requires us to define the CI integration workflow file `main.yml` in a new  
folder called `.github/workflows` off your project root (locally on your machine):

``` bash
(venv_spacewalks) $ mkdir -p .github/workflows
(venv_spacewalks) $ touch .github/workflows/main.yml
```

Now let's populate the `main.yml` file with our GitHub Actions workflow.

### Specify Workflow Name and When it Runs

So first let's specify a name for our workflow that will appear under GitHub Actions build reports,
and add the conditions that will trigger the workflow to run:

```yaml
name: CI

on: push
```

So here our workflow will run when changes are pushed to the repository.
There are [other events](https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows) we might specify instead (or as well) if we wanted,
but this one is the most common.

### Specify Structure to Contain Steps to Run on which Platform

GitHub Actions are described as a sequence of jobs (such as building our code, or running some tests),
and each job contains a sequence of steps
which each represent a specific "action" (such as running a command, or obtaining code from a repository).

Let's define the start of a workflow job we'll name `build-and-test` (which we could name anything we like):

```yaml
jobs:

  build-and-test:

    runs-on: ubuntu-latest
```

We only have one job in this workflow,
but we may have many.
We also specify the operating systems on which we want this job to run.
In this case, only the latest version of Linux Ubuntu,
but we could supply others too (such as Windows, or Mac OS) which we'll see later.

When the workflow is triggered,
our job will run within a `runner`,
which you can think of as a freshly installed instance of a machine running the operating system we indicate (in this case Ubuntu).

## Specify the Steps to Run

Let's now supply the concrete things we want to do in our workflow.
We can think of this as the things we need to set up and run on a fresh machine.
So within our workflow, we'll need to:

- Check out our code repository
- Install Python
- Install our Python dependencies (which is just `pytest` in this case)
- Run `pytest` over our set of tests

We can define these as follows:

```yaml
    steps:

    - name: Checkout repository
      uses: actions/checkout@v4

    - name: Set up Python 3.12
      uses: actions/setup-python@v5
      with:
        python-version: "3.12"
```

We first use GitHub Actions (indicated by `uses: actions/`),
which are small tools we use to perform something specific.
In this case, we use:

- `checkout` - to checkout the repository into our runner
- `setup-python` - to set up a specific version of Python

Note that the `name` entries are descriptive text and can be anything,
but it's good to make them meaningful since they are what will appear in our build reports as we'll see later.

```yaml
    - name: Install Python dependencies
      run: |
        python3 -m pip install --upgrade pip
        python3 -m pip install -r requirements.txt

    - name: Test with pytest
      run: |
        python3 -m pytest -v --cov
```

This workflow definition file instructs GitHub Actions to run our unit tests using Python version 3.12 each time code 
is pushed to our repository.

Finally, push these changes to your code repository to initiate running of tests on GitHub.

``` bash
(venv_spacewalks) $ git add .github/workflows/main.yml
(venv_spacewalks) $ git commit -m "Add GitHub actions workflow"
(venv_spacewalks) $ git push origin main
```

We've committed our workflow,
so how do we know its actually running?
Since the workflow is triggered on each `git push`,
if we go back to our main repository page,
we should see an orange circle next to the most recent commit displayed just above the directory contents.

On the left of this page a sidebar titled "Actions" lists all the workflows that are active in our repository. 
You should see "CI" here (which is the `name` of the workflow we just added to our repository).
The body of the page lists the outcome of all historic workflow runs. 
If the workflow was triggered successfully when we pushed to the repository, you should see one workflow run listed here.

When this workflow is complete, it will display either a green tick for success,
or a red cross if the workflow encountered an error.
You can also see a history of the past workflow runs' failures or successes for each workflow run triggered on the commits page,
by selecting `Commits` on the right of this most recent commit display.

For more detail we can check the progress of a running workflow by selecting `Actions` in the top navigation bar, e.g.

```         
    https://github.com/YOUR-REPOSITORY/actions
```

We can see here that a new run has started,
titled with our commit message.
This page also shows a historical log of any other previous workflow runs too.

We can also view a complete log of the output from workflow runs,
by selecting the first (and only) entry at the top of the list.
This will then display a list of our `job`s (in this case only `build-and-test`).
If we select `build-and-test` we'll see an in-progress log of our workflow run,
separated into separate collapsed steps that we may expand to view further detail.
Each of the steps is named from the `name` labels we gave each step.
Note that the workflow may still be running at this point,
so not all steps may be complete yet.

If we drill down by selecting the `Test with pytest` entry,
we'll get a breakdown of the thing we're really interested in,
which covers the output from running the `pytest` command in the workflow.

Now if we make a change to our code, our workflow will be triggered and these tests will run,
so let’s make a change.

## Summary

Our workflow will now be triggered every time a change to our code is pushed to our GitHub repository,
which means that our code is now always being checked against our tests.
Although we must remember to check the workflow log for this to have value.
We also need to be sure that our tests sufficiently verify the behaviour of our code as it evolves,
so we should ensure we update our tests as necessary,
and adding new tests as required to verify new functionality.

::: keypoints

- Continuous Integration can run tests automatically to verify changes as code develops in our repository.
- CI builds are typically triggered by commits pushed to a repository.
- We need to write a configuration file to inform a CI service what to do for a build.
- We can run - and get reports from - different CI infrastructure builds simultaneously.
- We should ensure our tests sufficiently verify code behaviour as it changes, and update them accordingly.

:::
