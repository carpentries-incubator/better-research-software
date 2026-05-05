## Episode: "Software for open and reproducible research"

### Exercise: 
### Tools and practices you use (5 min)

Individually,

- reflect on what practices or tools you are already using in your software development workflow,
- list some new practices or tools that you would like to start employing or using.

Write your reflections in the shared collaborative document.


### Exercise: 
### Assess the software project (10 min)

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

## Episode: Better start with a software project

### Exercise: 
#### Update filenames (5 min)

Try to make these changes yourself.

1. Give our Python script and input data file informative names - `eva_data_analysis.py` and `eva-data.json`, respectively.
2. Update other file names and paths used in the script - output CSV data (`eva-data.csv` to match the new input data name) and plot(`cumulative_eva_graph.png`).
3. Stage and commit these changes in the Git repository.

## Episode: Reproducible software environments
## Episode: Code readability

### Exercise: 
### Rename our variables to be more descriptive (5 min)

Let's apply this to `eva_data_analysis.py`.

a. Edit the code as follows to use descriptive (and consistent) variable names:

    - Change `data_f` to `input_file`
    - Change `data_t` to `output_file`
    - Change `g_file` to `graph_file`

    *Be sure to change all the occurrences of each variable name.*
b. What other variable names in our code would benefit from renaming? 
Rename these too. 
Hint: variables `w`, `t`, `tt` and `ttt` could also be renamed to be more descriptive.
c. Commit your changes to your repository. Remember to use an informative commit message.



### Exercise: 
### Remove an unused variable (2 min)

Find and remove an unused variable in our code. Then, commit the updated code to the git repo.


### Exercise: 
### Add comments to our code (10 min)

a. Examine `eva_data_analysis.py`.
Add as many comments as you think is required to help yourself and others understand what that code is doing.
b. Commit your changes to your repository. Remember to use an informative commit message.


### Exercise: 
### Extract functionality into a function (5 min)

Extract the code to plot a graph into a separate function `plot_cumulative_time_in_space(df, graph_file)`.
The function should take the following two arguments: 

1. a dataframe `df`, and 
2. a file object or a file path string `graph_file` where to save the plot.

Make sure to commit and push your changes.


### Exercise: 
### Writing docstrings (5 min)

Write docstrings for the functions `write_dataframe_to_csv` and `plot_cumulative_time_in_space` we introduced earlier.

## Episode: Code structure

### Exercise: 
### Project restructuring (10 min)

Restructure your software project so that input data is stored in `data/` directory and results (the graph and CSV data files) saved in `results/` directory off the project root. 

Remove current result files `eva-data.csv` and `cumulative_eva_graph.png` from the project root (if they exist) as they will be recreated by re-running the code.

Remember to create the `results/` empty directory before running the code or your code will fail.

## Episode: "Code correctness & testing"

### Exercise: 
### Types of software tests (3 min)

Fill in the blanks in the sentences below:

- \_\_\_\_\_\_\_\_\_\_ tests compare the \_\_\_\_\_\_ output of a
    program to its \_\_\_\_\_\_\_\_ output to demonstrate correctness.
- Unit tests compare the actual output of a \_\_\_\_\_\_
    \_\_\_\_\_\_\_\_ to the expected output to demonstrate correctness.
- \_\_\_\_\_\_\_\_\_\_ tests check that results have not changed since
    the previous test run.
- \_\_\_\_\_\_\_\_\_\_ tests check that two or more parts of a program
    are working together correctly.


### Exercise: 
### What are the limitations of informally testing code? (5 min)

Think about the questions below. Your instructors may ask you to share
your answers in a shared notes document and/or discuss them with other
participants.

- Why might we choose to test our code informally?
- What are the limitations of relying solely on informal tests to
  verify that a piece of code is behaving as expected?


### Exercise: 
### Interpreting pytest output (15 min)

A colleague has asked you to conduct a pre-publication review of their code which analyses time spent in space by various individual astronauts.

You tested their code using `pytest`, and got the following output.
Inspect it and answer the questions below.

#### Example `pytest` output

``` output
============================================================ test session starts 
platform darwin -- Python 3.12.3, pytest-8.2.2, pluggy-1.5.0
rootdir: /Users/Desktop/AnneResearcher/projects/Spacetravel
collected 9 items                                                                                                                                                              

tests/test_analyse.py FF....                                              [ 66%]
tests/test_prepare.py s..                                                 [100%]

====================================================================== FAILURES 
____________________________________________________________ test_total_duration

    def test_total_duration():
    
      durations = [10, 15, 20, 5]
      expected  = 50/60
      actual  = calculate_total_duration(durations)
>     assert actual == pytest.approx(expected)
E     assert 8.333333333333334 == 0.8333333333333334 ± 8.3e-07
E       
E       comparison failed
E       Obtained: 8.333333333333334
E       Expected: 0.8333333333333334 ± 8.3e-07

tests/test_analyse.py:9: AssertionError
______________________________________________________________________________ test_mean_duration 

    def test_mean_duration():
       durations = [10, 15, 20, 5]
    
       expected = 12.5/60
>      actual  = calculate_mean_duration(durations)

tests/test_analyse.py:15: 
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 

durations = [10, 15, 20, 5]

    def calculate_mean_duration(durations):
        """
        Calculate the mean of a list of durations.
        """
        total_duration = sum(durations)/60
>       mean_duration = total_duration / length(durations)
E       NameError: name 'length' is not defined

Spacetravel.py:45: NameError
=========================================================================== short test summary info 
FAILED tests/test_analyse.py::test_total_duration - assert 8.333333333333334 == 0.8333333333333334 ± 8.3e-07
FAILED tests/test_analyse.py::test_mean_duration - NameError: name 'length' is not defined
============================================================== 2 failed, 6 passed, 1 skipped in 0.02s 
```

a.  How many tests has our colleague included in the test suite?
b.  The first test in `test_prepare.py` has a status of `s`; what does this mean (search online to find out)?
c.  How many tests failed?
d.  Why did `test_total_duration` fail?
e.  Why did `test_mean_duration` fail?


### Exercise: 
### Unit tests for calculate_crew_size (10 min)

Implement unit tests for the `calculate_crew_size` function. 
Cover typical cases and edge cases.

Hint - use the following template when writing tests:

```python
def test_MYFUNCTION (): # FIXME
    """
    Test that ...   #FIXME
    """
    
    # Typical value 1
    actual_result =  _______________ #FIXME
    expected_result = ______________ #FIXME
    assert actual_result == expected_result
    
    # Typical value 2
    actual_result =  _______________ #FIXME
    expected_result = ______________ #FIXME
    assert actual_result == expected_result
    
```


### Exercise: 
### Evaluating code coverage (10 min)

Generate the code coverage report for your software using the `python3 -m pytest --cov --cov-report=html` command.

Inspect the `htmlcov` folder created by the above command in the root directory of your project, then open the 
`htmlcov/index.html` file in a Web browser and extract the following information:

a.  What proportion of the code base is currently "not" exercised by the test suite?
b.  Which functions in our code base are currently untested?

## Episode: Software documentation

### Exercise: 
### README and the FAIR principles  (10 min)

The following lists some of the major sections you may find in a typical README file.
Which are **essential** to support the [FAIR software][fair-principles-research-software] (Findable, Accessible, Interoperable, Reusable) principles and which are good to have but **optional**?

- Description and purpose of the code
- Audience (who the code is intended for)
- Installation instructions
- Pointers to dependencies and their versions (e.g. `requirements.txt` or `pyproject.toml`)
- Contribution guidelines
- How to get help
- License
- Software citation
- Usage examples
- FAQs
- Code of Conduct


### Exercise: 
### Spacewalks README (10 min)

Extend the README for Spacewalks by adding:

1. Installation instructions
2. A simple usage example


### Exercise: 
### Select a licence (10 min)

Choose a license for your code. 
Discuss with your neighbour or the group your choice of license and reason for choosing it.


### Exercise: 
### Add a license to your code (5 min)

Add a LICENSE file containing the full text of your chosen license to your code repository.

## Episode: My Software
## Episode: Spacewalks

### Exercise: 
### Spacewalks software citation (5 min)

Add the citation file for our Spacewalks software to the root folder of our repository on GitHub.
You can either do it directly on GitHub or creating the file locally and the committing and pushing to GitHub from the 
command line.

### Exercise: 
### Explore your documentation (5 min)

Explore documentation in `site/` folder built with MkDocs for your project, starting from the `index.html` file.

Open `index.html` file in a Web browser to see how it renders. 

Check `site/reference.html` to see how docstrings from your functions are provided here as a reference manual.


### Exercise: 
### Spacewalks how-to guide (15 min)

a. Review the Diataxis guidance page on writing a How-to guide. 
Identify three features of an effective how-to guide.

b. Following the Diataxis guidelines, add a how-to guide to the `docs/how-to-guides.md` file in your documentation folder to show users how to change the destination filename for the output CSV dataset generated by the Spacewalks software.


### Exercise: 
### Spacewalks tutorial (10 min)

Let's adapt the how-to guide from the previous challenge into a tutorial that explains 
how to change the file path for the output dataset when running the analysis script.


### Exercise: 
### Tutorial vs. how-to guide - discussion (5 min)

How does the content and language of our example tutorial differ from our example how-to guide?

## Episode: Software management & collaboration
## Episode: Spacewalks

### Exercise: 
### Practice with Issues and PRs (20 min)

We have a bug in our code! 
If we look at the results in `results/duration_by_astronaut.csv`, the crew column has groups of crew and we wanted to calculate this per astronaut. 

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
def summary_duration_by_astronaut(df):
    """
    Summarise the duration data by each astronaut and saves resulting table to a CSV file

    Args: 
        df (pd.DataFrame): Input dataframe to be summarised

    
    Returns:
        sum_by_astro (pd.DataFrame): Data frame with a row for each astronaut and a summarised column 
    """
    subset = df.loc[:,['crew', 'duration']] # subset to work with only relevant columns
    subset.crew = subset.crew.str.split(';').apply(lambda x: [i for i in x if i.strip()]) # splitting the crew into individuals and removing blank string splits from ending ;
    subset = subset.explode('crew') # separating lists of crew into individual rows
    subset = add_duration_hours(subset) # need duration_hours for easier calcs
    subset = subset.drop('duration', axis=1) # dropping the extra 'duration' column as it contains string values not suitable for calulations
    subset = subset.groupby('crew').sum() 
    return subset
```

## Episode: Wrap-up
