# The data diary

*very rough draft*


At the Associated Press, reporters use a standard form and format for every project that lets Meghan Hoyer, the unit's editor, dip into the work whenever she has time.

ProPublica data reporters are fact-checked by a colleague before publication. The second reporter tries to duplicate any important results using the descriptions provided by writing programs from scratch.

It doesn't matter where you come down on the esoteric debate on replication. No matter what, you're story has to be accurate and you need to be able to prove it. You also need to understand what you've done, why, and -- just as importantly -- where it all is.

## The nut
The formalized processes used by large teams or in-depth data analyses that form the basis of a piece that hinges on a statistical analysis might not make sense for smaller endeavors.

Almost all data work should be documented in at least the same detail that you keep track of your interview notes or transcripts and other research for any story. For data, though, we usually require even more detail -- enough so that someone reading through your diary would be able to duplicate your work  and understand what it means.

Think of this process as a note to your future self. Imagine that you had to stop work on your story halfway through, then were told to go back to it six months later. How could  you remember where you left off and what you'd already done?

In this module  you'll learn:

* The kinds of information you need to record in a data diary or in your documentation
* The questions you'll need to be able to answer before you publish
* A format for recording your work.

## Getting started

Before you even get started on a data-driven story, open up a new document and just start writing what you do. Here are some sections that are worth considering whenever you start a story or project.

For a quick daily story, you might be able to do everything in one short document. For a longer project, you may find it easier to break your documents apart into logical pieces.

In many cases, you can just link to a Jupyter notebook or R program that is self-documenting. That is, it's clear what the program does by reading it, and it's adequately commented to make sure you remember what you did.

### Data sourcing

* Where did you get the data? How do you know it's authentic?

* A description of who originally collects the data and why it exists.

* List of other stories that have used this or similar data -- links, advice, warnings and findings.

* Academic work that has relied on the data. Names, email addresses of those sources.

* Alternative sources for this and similar or related datasets or documents.

### Data documentation and  flaws

* Each step you took to look for flaws. For example, "Filtered on each field and looked for missing data." -- then what you found.

* Integrity checks you made with other sources; how they were reconciled.

* Links or copies of any original documentation such as a record layout, data dictionary or manual. If there isn't one, consider making a data dictionary with what you've learned.

* Questions about the meaning of fields or the scope of the data.

* Decisions you've made about the scope or method of your analysis. For example, if you want to look at "serious" crimes, describe how and why you categorized each crime as "serious" or "not serious." Some of these should be vetted by experts or should be verified by documenting industry standards.

* A list of interviews conducted / questions asked of officials and what they said.

### Processing notes

Some projects require many steps to get to a dataset that can be analyzed. You may have had to scrape the data, combine it with other sources or fix some entries. Some common elements you should document:

* Hand-made corrections. Try to list every one, but it's ok if you describe HOW you did it, such as clustering and hand-entering using OpenRefine. Link to any spreadsheet, document or program you used.

* Geocoding. Note how many were correct, how many missing, and what you did about it.

* A description of how you got messy data into a tabular form or a form suitable for analysis. For example, you may have had to strip headings or flip a spreadsheet on its head. Make sure to write down how you did that.

### The good part: Your analysis

 * Each question you asked of your data, and the steps you took to answer it. If you use programming notebooks, write it out in plain language before or after the query or statements.

 * Vetting of your answers: who has looked them over, commented on them

 * Why they might be wrong. 

## Examples of documentation  

[A published Jupyter notebook for an analysis of FEC enforcement](http://nbviewer.jupyter.org/github/datadesk/ferc-enforcement-analysis/blob/master/02_analyze.ipynb) actions from the Los Angeles Times' data desk.  Ben Welsh, the author of that notebook, says that there are previous with unpublishable work.

[An example of a data diary kept by Talia Buford](TB_Data_Diary.pdf), a ProPublica reporter, when she was working at the Center for Public Integrity. She's nicely annotated the document to show why she structures it the way she does.

[A 2018 Buzzfeed News repo with start-to-finish documentation](https://github.com/BuzzFeedNews/2018-05-fentanyl-and-cocaine-overdose-deaths) of and opiod death story.


## Data smells: looking for flaws in data

(NOTE: We will have another module addressing dirty data, how to find it and what to do about it.)

[An email exchange between Sarah Cohen and Craig Silverman](https://github.com/sarahcnyt/stabile/blob/master/docs/bulletproof.md), now at Buzzfeed, about the process she used at The New York Times in reporting and fact-checking. This isn't the same as a process for replication, but it discusses the kinds of things that should be in it.

[Ensuring Accuracy in Data Journalism, or *Data Smells*](https://github.com/nikeiubel/data-smells/wiki/Ensuring-Accuracy-in-Data-Journalism), by Nikolas Iubel
