# Group By

Like many newsrooms, reporters at St. Louis Public Radio heard the common story that violent crime goes up when the weather gets hot.

Brent Jones, a visual data journalist there, worked with a reporter and editor to find out.

"We were looking for a summer story, and have talked about putting more of a focus on gun violence," he said.

To do the story, Jones needed three things: police data, weather data, and knowing how to Group By. With data from the St. Louis Police Department, daily high temperature data from the National Weather Service, [the rest was just doing the analysis](https://github.com/stlpublicradio/2018-05-31-crime-and-heat-analysis/blob/master/crimes-and-heat.ipynb).

When they were done, they found the anecdotes were true: [crime in St. Louis does indeed edge higher when the temperature gets hotter](http://news.stlpublicradio.org/post/warm-weather-worries-st-louis-when-temperatures-rise-crime-often-follows#stream/0).


### The nut graph

Group By is one of the most basic, and most critical, skills in data analysis. It takes any number of things and groups them together by some common element. Imagine, if you will, you had a bag of Skittles candy spilled out on the table in front of you. Group By takes the yellow ones and puts them in a pile, and the green ones, and the purple ones, and so on.

The term Group By comes from databases -- specifically the Structured Query Language (SQL) command GROUP BY -- but it has analogues in every analysis platform out there.

In this module, you'll learn:

* The steps to grouping your data together
* An introduction to summarizations after you have grouped the data
* Ordering data to show differences

### The walkthrough

For this exercise, we're going to use an R library called dplyr, which is a library built for data analysis with a simple set of verbs. With all R libraries, first we must import it to use it. If you are unfamiliar with R, please work through the introductory module first.

```
library(dplyr)
```

And you need data. For this example, we're going to use a dataset of verified mountain lion sightings in Nebraska. The data is useful to provide context to stories of the big cats being spotted in places they aren't usually found -- particularly around Nebraska's major cities of Lincoln and Omaha. [Stories pop up](http://krvn.com/regional-news/woman-reports-mountain-lion-sighting-in-lincoln/) from time to time, but rarely include context. The state Game and Parks department keeps track of confirmed sightings. Let's look at that data.

We'll create a variable called `mountainlions` and populate it with the imported data using `read.csv`.

```
mountainlions <- read.csv("../../Data/mountainlions.csv")
```

And if we run `head(mountainlions)` -- a command to give us the headers and the first six records -- here is what we get.

    ID	Cofirm.Type	COUNTY	Date
    1	Track	Dawes	9/14/91
    2	Mortality	Sioux	11/10/91
    3	Mortality	Scotts Bluff	4/21/96
    4	Mortality	Sioux	5/9/99
    5	Mortality	Box Butte	9/29/99
    6	Track	Scotts Bluff	11/12/99


Note: We have four fields:
* ID, an number for each sighting
* A misspelled field that should be Confirm Type, which tells you how the state confirmed that it was a real mountain lion
* COUNTY, which is what you think it is.
* And Date, which is when the sighting occurred.

With this data, what is a logical question to ask? How about this one: Which counties have the most mountain lion sightings?

To answer that, we'll group them together using `group_by`. With dplyr, we can use a set of characters called pipes -- `%>%` to connect commands together. So, we'll take our dataframe, called `mountainlions` and pipe commands together. In this case, we're going to pipe together `group_by` and `summarize` because there's little use in just grouping things together. In all but the rarest of circumstances would you not summarize after grouping. With `summarize` we're going to simply count the number of things in each group.  

```
mountainlions %>%
  group_by(COUNTY) %>%
  summarise(
    count = n(),
  )
```

And we get back a longer version of this:

    COUNTY	count
    Banner	6
    Blaine	3
    Box Butte	4  
    Brown	15
    Buffalo	3
    Cedar	1
    Cherry	30
    Custer	8
    Dakota	3
    Dawes	111
    ...

Notice something? It's alphabetical order, not by the numbers. That's bothersome. We can fix that with ordering. In `dplyr`, that's through `arrange`. And since the default ordering is in ascending order -- smallest to largest -- we're going to add `desc` in front of the value we're going to sort by, which is `count`.

```
mountainlions %>%
  group_by(COUNTY) %>%
  summarise(
    count = n(),
  ) %>% arrange(desc(count))
```

And that will produce a table something like this:

    COUNTY	count
    Dawes	111
    Sioux	52  
    Sheridan 35
    Cherry   30
    Scotts Bluff	26
    Keya Paha	20
    Brown	15
    Rock	11
    Lincoln	10

Things to note:

* If you're not a Nebraska geography nerd, most of those counties are across the north and northwestern parts of the state in an area called the Pine Ridge.
* Lincoln, the city, is in Lancaster County. According to this data, there have been zero confirmed sightings in Nebraska's second most populous county. Omaha is in Douglas County, the state's most populous county, with two confirmed sightings.
* Look carefully at Sheridan County. Scan down the list of counties. See any problems? How might this affect your analysis?

### Resources for instructors

* Potential assignment: Use local or campus crime data to answer a series of questions. Examples: If you have multiple years of data, how many crimes were reported each year? What is the most common crime type? Which month has the most reported crime?
* Potential assignment: Use salary data from your city or university. Use group by and create the following summaries by job title: count, median and mean. Discuss the differences. For instance, my university salary data includes a very expensive football coach, a moderately expensive basketball coach, and a lot of well-paid assistant coaches before we get to chancellors and vice chancellors. How does that affect the numbers?

### Suggested reading

* Jones' [code analyzing crime and temperature data](https://github.com/stlpublicradio/2018-05-31-crime-and-heat-analysis/blob/master/crimes-and-heat.ipynb).
* [Notes on working with big-ish data](https://source.opennews.org/articles/notes-working-big-ish-data/)
