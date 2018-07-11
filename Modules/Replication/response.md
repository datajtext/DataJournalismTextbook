# A response to data journalism's replication obsession
**By Sarah Cohen**

A 2016 project in The New York Times Michael Schwirtz, Michael Winerip and Robert Gebeloff began like this: 

> The racism can be felt from the moment black inmates enter New York's upstate prisons. 
>
>They describe being called porch monkeys, spear chuckers and
>worse. There are cases of guards ripping out dreadlocks. One inmate,
>John Richard, reported that he was jumped at Clinton Correctional Facility by a guard who threatened
>to "serve up some black mashed potatoes with tomato sauce."

Inside the story were some damning data: an analysis by Gebeloff of nearly 60,000 disciplinary cases against inmates, internal reports and
parole decisions filled out the portrait the reporters had seen on the ground: At every phase of the justice system in New York,
blacks fared worse than whites. The story was a [finalist for the 2017 Pulitzer Prize for Local Reporting](http://www.pulitzer.org/finalists/michael-schwirtz-michael-winerip-and-robert-gebeloff). 

After the story ran, Gebeloff spent more than a week preparing datasets that [could be published](https://github.com/newsdev/nyt_inmates)
without unnecessarily naming inmates and that could be run through standard statistical tests.

That week -- time that most news organizations would not support -- 
started at the end of Gebeloff's data journey. For example, the disciplinary file that the state provided under the FOIL law didn't
include any demographic information on the inmates. For that, Gebeloff had to scrape the state's corrections database and link up 
the prisoner numbers from the original. He also removed  personally identifiable details redacted. He led a reader through the data he produced, which in the end were rather simple rates across a broad set of measures.  

The key to this story and many others was Gebeloff's imaginiation in sussing out data sources to answer a question, 
not analyzing a static dataset. The available data confirmed the deep on-the-ground reporting. It was context, not proof.

And there lies the problem in linking data journalism too closely to science. In the end, we're not scientists -- we're storytellers. 

## Best practices

So what's a good reporter to do? Waite suggests ditching spreadsheets and working entirely in self-documenting code. That's a great idea for reporters who know how. And everyone should be able to walk through everything they've done in a dataset and reproduce their answers. But most of the mistakes I've seen in data journalism aren't from pressing the wrong buttons, but from choosing to analyze the wrong records, or failing to ground-truth what the reporter found.

One approach to the replicability problem, both inside and outside the newsroom, is to maintain a detailed data diary. This document, which can get quite long, documents the source of all of the data you considered, what you did to try to get it, how you edited or cleaned it, and how you checked it against the real world. It also documents the experts and other people you consulted on how to work with the data or what it means. And, of course, it documents the queries, spreadsheets and other tools used to produce any finished conclusions. 

Replicability is essential for complicated data analyses that apply novel or difficult methodologies to come to a conclusion. It's helpful for other reporters and analysts who want to learn how to do the analysis. And transparency -- where the data came from and how it was used -- is essential for credibility. That should be enough.




