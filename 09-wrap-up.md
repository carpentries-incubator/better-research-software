---
title: Wrap-up
teaching: 45
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions 

- What are the FAIR research principles?
- How do FAIR principles apply to software?
-  What are the wider Research Software Development Principles and where does FAIR fit into them?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

After completing this episode, participants should be able to:

- Explain the FAIR research principles in the context of research software
- Explain why these principles are of value in the research community 
- Reflect on the Research Software Development Principles and their relevance to own research.

::::::::::::::::::::::::::::::::::::::::::::::::

The good development practices taught in this lesson will help you build better research software.
The [final branch](https://github.com/carpentries-incubator/bbrs-software-project/tree/final) of the software project repository contains an improved version of the example code after good practices have been applied.
Some may require time and perseverance to implement and embed in your routine. 
Others are small changes you can start practicing today.

![An image of a Chinese proverb "The best time to plant a tree was 20 years ago. The second best time is now" by CCNULL, used under a CC-BY 2.0 licence](episodes/fig/plant-a-tree.jpg){alt='An image of a Chinese proverb "The best time to plant a tree was 20 years ago. The second best time is now'}

## FAIR Research Software
One framework that can help you evaluate the alignment of a piece of research software with best practices in reproducibility are the _FAIR Principles for Research Software_.
The practices taught here fall within this framework and it can be a good place to find out what else you can start doing to improve even further.

### What is FAIR?

FAIR stands for Findable, Accessible, Interoperable, and Reusable and comprises a set of principles designed to
increase the visibility and usefulness of your research to others.
The FAIR data principles, first published [in 2016][fair-data-principles], are widely known and applied today.
Similar [FAIR principles for software][fair-principles-research-software] have now been defined too. In general, they mean:

- **Findable** - software and its associated metadata must be easy to discover by humans and machines.
- **Accessible** - in order to reuse software, the software and its metadata must be retrievable by standard protocols, free and legally usable.
- **Interoperable** - when interacting with other software it must be done by exchanging data and/or metadata through
  standardised protocols and application programming interfaces (APIs).
- **Reusable** - software should be usable (can be executed) and reusable
  (can be understood, modified, built upon, or incorporated into other software).

Each of the above principles can be achieved by a number of practices listed below.
This is not an exact science, and by all means the list below is not exhaustive,
but any of the practices that you employ in your research software workflow will bring you
closer to the gold standard of fully reproducible research.

#### Findable
- Create a description of your software to make it discoverable by search engines and other search tools
- Use standards (such as [CodeMeta][codemeta]) to describe interoperable metadata for your software (see [Research Software Metadata Guidelines][rsmd-g1])
- Place your software in a public software repository (and ideally register it in a [general-purpose or domain-specific software registry][awesome-rs-registries])
- Use a unique and persistent identifier (DOI) for your software (e.g. by depositing your code on [Zenodo][zenodo]),
  which is also useful for citations - note that depositing your data/code on GitHub and similar software repositories
  may not be enough as they may change their open access model or disappear completely in the future, so archiving your code means it stands a better chance at being preserved

#### Accessible
- Make sure people can obtain get a copy your software using standard communication protocols (e.g. HTTP(S), (S)FTP, etc.)
- The code and its description (metadata) has to be available even when the software is no longer actively developed (this includes earlier versions of the software)

#### Interoperable
- Use community-agreed standard formats for inputs and outputs of your software and its metadata
- Communicate with other software and tools via standard protocols and APIs

#### Reusable
- Document your software (including its functionality, how to install and run it) so it is both usable (can be executed) 
and reusable (can be understood, modified, built upon, or incorporated into other software)
- Give a licence to your software clearly stating how it can be reused

:::::: callout

### FAIR is a process, not a perfect metric

FAIR is not a binary metric - there is no such thing as "FAIR or "not FAIR".

FAIR is not a perfect metric, nor does it provide a full and exhaustive software quality checklist - there are other good software quality practices not covered by FAIR. 
Conversely, software may be FAIR but still not very good in terms of its functionality.

FAIR is **not meant** to criticise or discredit work. 

FAIR refers to the specific **values** of and describes a set of **principles** to aid open and reproducible research that can be a helpful guide for researchers who want to improve their practices (by helping them see where they are on the **FAIR spectrum** and help them on a **journey** to make their software more FAIR). 

::::::

::::::::::::::::::::::::::::::::::::: checklist

### Assessing the FAIRness of your Research Software

Here are some questions to help you assess where on the FAIR spectrum your software is.

1. **Findable**
  * If these files were emailed to you, or sent on a chat platform, or handed to you on a memory stick, how easy would it be to find them again in 6 months, or 3 years?
  * If you asked your collaborator to give you the files again later on, how would you describe them? Do they have a clear name? 
  * If more data was added to the data set later, could you explain exactly which data you used in the original analysis?
2. **Accessible**
  * If the person who gave you the files left your institution, how would you get access to the files again?
  * Once you have the files, can you understand the code? Does it make sense to you?
  * Do you need to log into anything to use this? Does it require purchase or subscription to a service, platform or tool?
3. **Interoperable**
  * Is it clear what kind of input data it can read and what kind of output data is produced? Will you be able to create the input files and read the output files with the tools your community generally uses? 
  * If you wanted to use this tool as part of a larger data processing pipeline, does it allow you to link it with other tools in standard ways such as an API or command-line interface?
4. **Reusable**
  * Can you run the code on your platform/operating system (is there documentation that covers installation instructions)? What programs or libraries do you need to install to make it work (and which versions)? Are these commonly used tools in your field?
  * Do you have explicit permission to use your collaborators code in your own research and do they expect credit of some form (paper authorship, citation or acknowledgement)? Are you allowed to edit, publish or share the files with others?
  * Is the language used familiar to you and people in your research field? Can you read the variable names in the code and the column names in the data file and understand what they mean?
  * Is the code written in a way that allows you to easily modify or extend it? Can you easily see what parameters to change to make it calculate a different statistic, or run on a different input file?

::::::::::::::::::::::::::::::::::::::::::::::::

### FAIR Software is Better Software
You may or may not find the FAIR Research Software Principles a helpful way of framing good practices.
The important thing is to focus on how **adopting these individual ways of working contributes to making your software better**.
Many of the practices taught here -- and advocated for in the FAIR framework -- will make your improve your life as a researcher and software developer.

The table below provides a summary of some good practices for developing research software, together with different tools that can help with such practices and how they contribute to the the FAIR and other good software principles.

| Practices                                                                        | Tools                                                                                                                                    | FAIR | Readable/Understandable | Correct/Reliable  | Sustainable/Maintainable |
|----------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|------|-------------------------|-------------------|--------------------------|
| Use version control                                                              | `git`, GitHub, GitLab, BitBucket                                                                                                         | F    |                         |                   |                          |
| Write modular code with well defined interfaces                                   |                                                                                                                                          | R    | x                       |                   | x                        |
| Connect reusable software components into automated/reproducible software pipelines | Command line tools, CLI, workflow tools (Galaxy, Snakemake, WorkflowHub, CWL)                                                            | I, R |                         |                   |                          |
| Use reproducible software development environments                               | `venv`, `conda`, IDEs (integration with virtual envs.), Docker, etc.                                                                     | R    |                         |                   |                          |
| Use conventional folder structures, format your code to comply with coding conventions                               | PEP8, IDEs (help with formatting and conforming with coding conventions)                                                                 | R    |                         |                   |                          |
| Use standard exchange data formats/communication protocols/interfaces            | CSV, YAML, JSON, CLI, REST, HTTP(S), etc.                                                                                                | I    |                         |                   | x                        |
| Test your software                                                               | Unit, functional, integration, regression, etc. tests, IDEs (testing and debugging), CI/CD (automation) |      |                         | x                 |                          |
| Document your software                                                           | Comments and documentation strings, README, guides, contributions guidelines                                                             | R    | x                       |                   |                          |
| Share your software & encourage review                                           | Code sharing platforms/services (e.g. GitHub, GitLab, BitBucket) and their code review facilities                                        | F, A |                         |                   | x                        |
| License your software                                                            | Various open source licences for code (MIT, BSD, GPL, LGPL, etc.), LICENSE                                                               | R    |                         |                   |                          |
| Use persistent identifiers for your software                                     | DOIs, SWHIDs, Zenodo, FigShare, Software Heritage, etc.                                                                                  | F    |                         |                   | x                        |
| Provide citation & metadata info for your software                               | CITATION, DOIs, Zenodo, CFF, `cffinit`, CodeMeta, etc.                                                                                   | R    |                         |                   | x                        |
| Build community & encourage collaboration around your software                   | Code of Conduct, README, CONTRIBUTING, open source project governance processes                                                          |      |                         |                   | x                        |

Best practices are always evolving and there is usually more we could be doing to make our software even better, even more reproducible, even FAIRer.
The skills and techniques introduced in this lesson are a great place to start! 

:::::::::::::::::::::: callout

## Tools for assessing FAIRness

Here are some tools that can check your software and provide an assessment of its FAIRness:

- [FAIRsoft evaluator][fair-rs-evaluator]
- [FAIR software test][fair-rs-test]
- [`How FAIR is your software` - command line tool to evaluate a software repository's compliance with the FAIR principles][howfairis]

::::::::::::::::::::::::::::::


## Research software development principles

Software and people who develop it have significance within the research environment and a broader impact on society and the planet.
FAIR research software principles cover some aspects and operate within the wider [**Research Software Development Principles**](https://rsecon24.society-rse.org/about/research-software-development-principles/) - recommended by Software Sustainability Institute's Director Neil Chue Hong during his [keynote at RSECon23](https://rsecon24.society-rse.org/about/research-software-development-principles/#neil-chue-hong-rse23-keynote).
These principles can help us explore and reflect on our own work and guide us on a path to better research.

### Helping your team

![Helping your team, image from RSECon2024, used under CC BY 4.0](episodes/fig/help-the-team.png){alt='Help the team principles of writing FAIR, secure and maintainable code'}

### Helping you peers

![Helping your peers, image from RSECon2024, used under CC BY 4.0](episodes/fig/help-the-peers.png){alt='Help the peers principles of making your work reproducible, inclusive and credit everyone involved'}

### Helping the world

![Helping the world, image from RSECon2024, used under CC BY 4.0](episodes/fig/help-the-world.png){alt='Help the world principles of being responsible, open and global, and humanist when developing research software'}

## Further reading

We recommend the following resources for some additional reading on FAIR Research Software:

- ["Five recommendations for FAIR software"][5-fair-software-recommendations]
- ["10 easy things to make your research software FAIR"][10-easy-fair-things]
- ["Ten simple rules for training scientists to make better software"][10-rules-better-software]
- [Automating assessment of the FAIR Principles for Research Software (FAIR4RS)][automated-assessment-fairrs]
- [Short online courses][nesc-rs-support-courses] on various aspects of research software 
(including [FAIR research software][nesc-rs-support-course-fair] and data), by the NeSC Research Software Support
- [CodeRefinery][coderefinery] - training and e-Infrastructure for research software development
- A [self-assessment checklist for FAIR research software][fair-rs-checklist], by the Netherlands eScience Center
    and Australian Research Data Commons 
- [Awesome Research Software Registries][awesome-rs-registries] - a list of research software 
registries (by country, organisation, domain and programming language) where research software can be registered 
to help promote its discovery

Please check out [the following resources](learners/reference.md#litref) for some additional reading 
on the topic of this course and the full reference set.

:::::::::::::::::::::::::::::::::::::::: keypoints

- FAIR data and software is Findable, Accessible, Interoperable, Reusable.
- These principles support research and researchers by saving time, reducing barriers to discovery, and increasing impact of the research output.
- When developing software for your research, think about how it will help you and your team, your peers and domain/community and 
the world.

::::::::::::::::::::::::::::::::::::::::::::::::::
