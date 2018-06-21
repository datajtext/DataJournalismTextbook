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

For this exercise, we're going to use a Python library called Pandas, which is a widely used data analysis library. With all Python libraries, first we must import it to use it. If you are unfamiliar with Python, please work through the introductory Python module first.

A common convention in Pandas is to rename it on import to make typing easier.

```
import pandas as pd
```

And you need data. For this example, we're going to use a dataset of verified mountain lion sightings in Nebraska. The data is useful to provide context to stories of the big cats being spotted in places they aren't usually found -- particularly around Nebraska's major cities of Lincoln and Omaha. [Stories pop up](http://krvn.com/regional-news/woman-reports-mountain-lion-sighting-in-lincoln/) from time to time, but rarely include context. The state Game and Parks department keeps track of confirmed sightings. Let's look at that data.

We'll create a variable called `mountainlions` and populate it with the imported data using `pd.read_csv`.

```
mountainlions = pd.read_csv('../../Data/mountainlions.csv')
```

If we execute `mountainlions.head()` we get:

```
    ID	Cofirm Type	COUNTY	Date
0	1	Track	Dawes	9/14/91
1	2	Mortality	Sioux	11/10/91
2	3	Mortality	Scotts Bluff	4/21/96
3	4	Mortality	Sioux	5/9/99
4	5	Mortality	Box Butte	9/29/99
```
Note: We have four fields:
* ID, an number for each sighting
* A misspelled field that should be Confirm Type, which tells you how the state confirmed that it was a real mountain lion
* COUNTY, which is what you think it is.
* And Date, which is when the sighting occurred.

With this data, what is a logical question to ask? How about this one: Which counties have the most mountain lion sightings?

To answer that, we'll group them together using `group_by`.

```
mountainlions.groupby(["COUNTY",])
```

If we do that, you'll see that we get something not very useful. It looks something like:

```
<pandas.core.groupby.groupby.DataFrameGroupBy object at 0x10e184048>
```
Which means we have a data frame, a table, of grouped objects. It means we have to do something to that data frame to make it useful. Something like count each thing.

```
mountainlions.groupby(["COUNTY",]).size()
```
That's more like it.

```
COUNTY
Banner            6
Blaine            3
Box Butte         4
Brown            15
Buffalo           3
Cedar             1
Cherry           30
Custer            8
Dakota            3
Dawes           111
Dawson            5
Dixon             3
Douglas           2
Frontier          1
Hall              1
Holt              2
Hooker            1
Howard            3
Keith             1
Keya Paha        20
Kimball           1
Knox              8
Lincoln          10
Merrick           1
Morrill           2
Nance             1
Nemaha            5
Platte            1
Polk              1
Richardson        2
Rock             11
Sarpy             1
Saunders          2
Scotts Bluff     26
Sheridan         35
Sherman           1
Sioux            52
Thomas            5
Thurston          1
Valley            1
Wheeler           1
sheridan          2
```

 But it's not in order, so it is sort of bothersome. We can fix that with ordering. Now, with Pandas, we have to tell it that we want to reorder it from it's initial ordering. So we have to use something called `reset_index` and tell it which column we're going to reset it with. Then, we can sort the column using `sort_values`. The default setting in sorting is ascending order -- smallest to largest -- so we need to tell it that we don't want that. Like many things in Python, we do it with setting a boolean to `False`. That's a lot to preamble, but it's fairly simple when implemented.

```
mountainlions.groupby(["COUNTY",]).size().reset_index(name="count").sort_values("count", ascending=False)
```

And that gives us our answer.

```
COUNTY	count
9	Dawes	111
36	Sioux	52
34	Sheridan	35
6	Cherry	30
33	Scotts Bluff	26
19	Keya Paha	20
3	Brown	15
30	Rock	11
22	Lincoln	10
21	Knox	8
7	Custer	8
0	Banner	6
26	Nemaha	5
37	Thomas	5
10	Dawson	5
2	Box Butte	4
4	Buffalo	3
17	Howard	3
11	Dixon	3
8	Dakota	3
1	Blaine	3
12	Douglas	2
32	Saunders	2
29	Richardson	2
41	sheridan	2
15	Holt	2
24	Morrill	2
25	Nance	1
16	Hooker	1
40	Wheeler	1
39	Valley	1
38	Thurston	1
14	Hall	1
35	Sherman	1
5	Cedar	1
18	Keith	1
31	Sarpy	1
20	Kimball	1
23	Merrick	1
28	Polk	1
13	Frontier	1
27	Platte	1
```

Things to note:

* If you're not a Nebraska geography nerd, most of those counties are across the north and northwestern parts of the state in an area called the Pine Ridge.
* Lincoln, the city, is in Lancaster County. According to this data, there have been zero confirmed sightings in Nebraska's second most populous county. Omaha is in Douglas County, the state's most populous, with two confirmed sightings.
* Look carefully at Sheridan County. Scan down the list of counties. See any problems? How might this affect your analysis?

### Resources for instructors

* Potential assignment: Use local or campus crime data to answer a series of questions. Examples: If you have multiple years of data, how many crimes were reported each year? What is the most common crime type? Which month has the most reported crime?
* Potential assignment: Use salary data from your city or university. Use group by and create the following summaries by job title: count, median and mean. Discuss the differences. For instance, my university salary data includes a very expensive football coach, a moderately expensive basketball coach, and a lot of well-paid assistant coaches before we get to chancellors and vice chancellors. How does that affect the numbers?

### Suggested reading

* Jones' [code analyzing crime and temperature data](https://github.com/stlpublicradio/2018-05-31-crime-and-heat-analysis/blob/master/crimes-and-heat.ipynb).
* [Notes on working with big-ish data](https://source.opennews.org/articles/notes-working-big-ish-data/)
