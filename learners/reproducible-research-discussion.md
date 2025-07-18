---
title: Reproducible Research Discussion
---

## Jargon busting
Before we start with the course, below we cover the terminology and explain terms, phrases, and 
concepts associated with software development in reproducible research that we will use in this course.

* **Reproducibility** - the ability to be reproduced or copied; the extent to which consistent results are obtained 
when an experiment is repeated (definition from [Google’s English dictionary is provided by Oxford Languages][google-oxford-dict])
* **Computational reproducibility** - obtaining consistent results using the same input data, computational methods (code),
and conditions of analysis; work that can be independently recreated from the same data and the same code 
([definition][ttw-reproducibility-def] 
by the [Turing Way's "Guide to Reproducible Research"][ttw-guide-reproducible-research])
* **Reproducible research** - the idea that scientific results should be documented in such a way that their deduction
is fully transparent ([definition][wiki-reproducibility-def] from Wikipedia)
* **Open research** - research that is openly accessible by others; concerned with making research more transparent, 
more collaborative, more wide-reaching, and more efficient 
([definition][wiki-open-research-def] from Wikipedia)
* **FAIR** - an acronym that stands for Findable, Accessible, Interoperable, and Reusable
* **Sustainable software development** - software development practice that takes into account longevity and 
maintainability of code (e.g. beyond the lifetime of the project), environmental impact, societal responsibility and ethics in 
our software practices. 

:::::::::::::::::::::::::::::::::::::::: callout
## Computational reproducibility

In this course, we use the term "reproducibility" as a synonym for "computational reproducibility".
:::::::::::::::::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::: discussion

### Motivation
Think about the questions below. Your instructors may ask you to share your answers in a shared notes document and/or
discuss them with other participants.

- What motivated you to attend this course? Did you come by choice or were you advised to attend?
- What do you hope to learn or change in your current research software practice? Describe how your knowledge,
  work or attitude may be different afterwards.

::::::::::::::::::::::::::::::::::::::::::::::::

## What is reproducible research?

[The Turing Way's "Guide to Reproducible Research"][ttw-guide-reproducible-research]
provides an [excellent overview of definitions of "reproducibility" and "replicability"][ttw-reproducibility-def] found in literature, 
and their different aspects and levels. 

In this course, we adopt the Turing Way's definitions: 

* **Reproducible research**: a result is reproducible when the same analysis steps performed on the same data 
consistently produce the same answer.
  * For example, two different people drop a pen 10 times each and every time it falls to the floor. Or, we run the same code multiple times on different machines and each time it produces the same result.
* **Replicable research**: a result is replicable when the same analysis performed on different data produces 
qualitatively similar answers.
  * For example, instead of a pen, we drop a pencil, and it also falls to the floor. Or, we collect two different datasets as part of two different studies and run the same code over these datasets with the same result each time. 
* **Robust research**: a result is robust when the same data is subjected to different analysis workflows to answer the 
same research question and a qualitatively similar or identical answer is produced.
  * For example, I lend you my pen and you drop it out the window, and it still falls to the floor. Or we run the same analysis implemented in both Python and R over the same data and it produces the same result.
* **Generalisable research**: combining replicable and robust findings allow us to form generalisable results 
that are broadly applicable to different types of data or contexts.
  * For example, everything we drop - falls, therefore gravity exists.

![*The Turing Way project illustration of aspects of reproducible research by Scriberia, used under a CC-BY 4.0 licence, [DOI: 10.5281/zenodo.3332807][ttw-illustrations]*](https://raw.githubusercontent.com/the-turing-way/the-turing-way/refs/heads/main/book/website/figures/reproducible-definition-grid.svg){alt='Four cartoon images depicting two researchers at two machines which take in data and output the same landscape image in 4 different ways. These visually describe the four scenarios listed above.'}

In this course we mainly address the aspect of reproducibility - i.e. enabling others to run our code to obtain the same results.

We can also further differentiate between:

* **Computational reproducibility**: when detailed information is provided about code, software, hardware and 
implementation details.
* **Empirical reproducibility**: when detailed information is provided about non-computational empirical scientific 
experiments and observations. In practice, this is enabled by making the data and details of how it was 
collected freely available.
* **Statistical reproducibility**: when detailed information is provided, for example, about the choice of 
statistical tests, model parameters, and threshold values. This mostly relates to pre-registration of study design to prevent p-value hacking and other manipulations.

In this course, we are concerned with computational reproducibility, i.e. when the application of computer science and 
software engineering is used to aid solving research problems.


::::::::::::::::::::::::::::::::::::: discussion

### What do the terms open and reproducible research mean to you?
Think about the questions below. Your instructors may ask you to share your answers in a shared notes document and/or
discuss them with other participants.

- How would you define the words "open" and "reproducible" in the context of research?
- Who might benefit from your work being open and reproducible? *Think about both groups and individuals.*
- Have you wished that someone else's work was more open or accessible to you? What did you do in that instance? Why do you think the author didn't make their work more open or accessible?
- Have you ever gone back to an old project and struggled to understand what you did or why? How did that feel?  Were you able to find the information you needed?

::::::::::::::::::::::::::::::::::::::::::::::::


## Why do reproducible research?

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


## Research Software
However, it is important to note that not all software that is used in research is "research software". 
We define "research software" as software or code that is used to generate, process or analyse results of a research for publication. 
For example, software used to guide a telescope is not considered "research software". 
On the other hand, formulas or macros in spreadsheets used to analyse data are considered "research code" as they are a form of computer programming that allow one to create, calculate, and change data sets in a number of different ways.

![*Definition of "research software" from the FAIR4RS working group, image by the Netherlands eScience Center licensed under CC-BY 4.0*](https://raw.githubusercontent.com/esciencecenter-digital-skills/research-software-support/611da359cbe1d04ecf056545ee07f977ae536273/modules/researchsoftware/media/definition.png){alt='Quote: Research Software includes source code files, algorithms, scripts, computational workflows and executables that were created during the research process or for a research purpose. Software components (e.g., operating systems, libraries, dependencies, packages, scripts, etc.) that are used for research but were not created during or with a clear research intent should be considered software in research and not Research Software.'}

In the [software survey conducted by the Software Sustainability Institute in 2014][ssi-survey-2014], 92% of researchers indicated they used some kind of software to aid or conduct their research.
This was not limited to researchers from [computational science][computational-science] (aka scientific computing), the "hard" sciences or to those involved in “traditional” uses of computing infrastructure such as running simulations or developing computational methods.
The **use of research software is ubiquitous and fairly even across all disciplines**.

Research software is increasingly being developed - researchers do not just use “off the shelf” software and the majority of researchers develop their own. 
In order to be able to produce quality software that outputs correct and verifiable results and that can be reused over time - researchers require training.
