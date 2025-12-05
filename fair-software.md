## FAIR Research Software

One framework that can help you evaluate the alignment of a piece of research software with best practices in reproducibility are the _FAIR Principles for Research Software_.
The practices taught here fall within this framework and it can be a good place to find out what else you can start doing to improve even further.

### What is FAIR?

FAIR stands for Findable, Accessible, Interoperable, and Reusable and comprises a set of principles designed to
increase the visibility and usefulness of your research to others.
The [FAIR data principles][fair-data-principles], first published in 2016, are widely known and applied today.
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

- Make sure people can obtain get a copy of your software using standard communication protocols (e.g. HTTP(S), (S)FTP, etc.)
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

- If these files were emailed to you, or sent on a chat platform, or handed to you on a memory stick, how easy would it be to find them again in 6 months, or 3 years?
- If you asked your collaborator to give you the files again later on, how would you describe them? Do they have a clear name?
- If more data was added to the data set later, could you explain exactly which data you used in the original analysis?

2. **Accessible**

- If the person who gave you the files left your institution, how would you get access to the files again?
- Once you have the files, can you understand the code? Does it make sense to you?
- Do you need to log into anything to use this? Does it require purchase or subscription to a service, platform or tool?

3. **Interoperable**

- Is it clear what kind of input data it can read and what kind of output data is produced? Will you be able to create the input files and read the output files with the tools your community generally uses?
- If you wanted to use this tool as part of a larger data processing pipeline, does it allow you to link it with other tools in standard ways such as an API or command-line interface?

4. **Reusable**

- Can you run the code on your platform/operating system (is there documentation that covers installation instructions)? What programs or libraries do you need to install to make it work (and which versions)? Are these commonly used tools in your field?
- Do you have explicit permission to use your collaborators code in your own research and do they expect credit of some form (paper authorship, citation or acknowledgement)? Are you allowed to edit, publish or share the files with others?
- Is the language used familiar to you and people in your research field? Can you read the variable names in the code and the column names in the data file and understand what they mean?
- Is the code written in a way that allows you to easily modify or extend it? Can you easily see what parameters to change to make it calculate a different statistic, or run on a different input file?

::::::::::::::::::::::::::::::::::::::::::::::::

### FAIR Software is Better Software

You may or may not find the FAIR Research Software Principles a helpful way of framing good practices.
The important thing is to focus on **how adopting these individual ways of working contributes to making your software better**.
Many of the practices taught here -- and advocated for in the FAIR framework -- will make your improve your life as a researcher and software developer.