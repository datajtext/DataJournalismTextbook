# Group By

Like many newsrooms, reporters at St. Louis Public Radio heard the anecdote that violent crime goes up when the weather gets hot.

Brent Jones, a visual data journalist there, worked with a reporter and editor to find out.

"We were looking for a summer story, and have talked about putting more of a focus on gun violence," he said.

To do the story, Jones needed three things: police data, weather data, and knowing how to Group By.

When they were done, they found the anecdotes were true: [crime in St. Louis does indeed edge higher when the temperature gets hotter](http://news.stlpublicradio.org/post/warm-weather-worries-st-louis-when-temperatures-rise-crime-often-follows#stream/0).


### The nut graph

Group By is one of the most basic, and most critical, skills in data analysis. It takes any number of things and groups them together by some common element. Imagine, if you will, you had a bag of Skittle candy spilled out on the table in front of you. Group By takes the yellow ones and puts them in a pile, and the green ones, and the purple ones, and so on.

In this module, you'll learn:

* The steps to grouping your data together
* An introduction to summarizations after you have grouped the data
* Ordering data to show differences

### The walkthrough

For this exercise, we're going to use a Python library called Agate, which is an analysis library built for data journalists. With all Python libraries, first we must import it to use it. If you are unfamiliar with Python, please work through the introductory python module first.

```
import agate
```

And you need data. For this example, we're going to use a dataset of verified mountain lion sightings in Nebraska. The data is useful to provide context to stories of the big cats being spotted in places they aren't usually found -- particularly around Nebraska's major cities of Lincoln and Omaha. [Stories pop up](http://krvn.com/regional-news/woman-reports-mountain-lion-sighting-in-lincoln/) from time to time, but rarely include context. The state Game and Parks department keeps track of confirmed sightings. Let's look at that data.

We'll create a variable called `mountainlions` and populate it with the imported data using `agate.Table.from_csv`.

```
mountainlions = agate.Table.from_csv('../../Data/mountainlions.csv')
print(mountainlions)
```

And here is what we get.

    |---------------+---------------|
    |  column_names | column_types  |
    |---------------+---------------|
    |  ID           | Number        |
    |  Cofirm Type  | Text          |
    |  COUNTY       | Text          |
    |  Date         | Date          |
    |---------------+---------------|

Note: We have four fields:
* ID, an number for each sighting
* A misspelled field that should be Confirm Type, which tells you how the state confirmed that it was a real mountain lion
* COUNTY, which is what you think it is.
* And Date, which is when the sighting occurred.

With this data, what is a logical question to ask? How about this one: Which counties have the most mountain lion sightings?

To answer that, we'll group them together using `group_by`. We'll create a new table, called `by_county` and populate it with the results of our `group_by` statement. The new table is a subset of our first table we created on import, so we'll have to be sure to use that.

```
by_county = mountainlions.group_by('COUNTY')
print(len(by_county))
```

And we get back 42. That means 42 counties had mountain lion sightings out of 93 Nebraska counties. That's a chunk. However, it helps to know what by using `group_by` in Agate, we haven't actually created a new table. We've created a TableSet. Which is why you can't print it and see it.


```
by_county.print_table()
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <i-input-9-27a489864901> in <module>()
    ----> 1 by_county.print_table()


    /Users/mattwaite/anaconda/envs/homework/lib/3.5/site-packages/agate/tableset.py in __getattr__(self, name)
        115         # Proxy table methods
        116         if name in Table.__dict__:
    --> 117             if Table.__dict__[name].allow_tableset_proxy:
        118                 return TableMethodProxy(self, name)
        119


    AttributeError: 'function' object has no attribute 'allow_tableset_proxy'


To make something out of a `group_by` TableSet, we have to run some aggregates on it. The most basic aggregate, one used all the time by data analysts, is the simple count -- how many things do I have in my group of things. Or, in our case, how many sightings were there in each county?  

```
county_totals = by_county.aggregate([
    ('count', agate.Count())
])

county_totals.print_table()
```

This is what we get.

    |---------------+--------|
    |  COUNTY       | count  |
    |---------------+--------|
    |  Dawes        |   111  |
    |  Sioux        |    52  |
    |  Scotts Bluff |    26  |
    |  Box Butte    |     4  |
    |  Howard       |     3  |
    |  Brown        |    15  |
    |  Douglas      |     2  |
    |  Cherry       |    30  |
    |  Thomas       |     5  |
    |  Keya Paha    |    20  |
    |  Dakota       |     3  |
    |  Sarpy        |     1  |
    |  Custer       |     8  |
    |  Sheridan     |    35  |
    |  Banner       |     6  |
    |  Knox         |     8  |
    |  Nance        |     1  |
    |  Platte       |     1  |
    |  Dawson       |     5  |
    |  Rock         |    11  |
    |  Hooker       |     1  |
    |  Lincoln      |    10  |
    |  Polk         |     1  |
    |  Valley       |     1  |
    |  Sherman      |     1  |
    |  Blaine       |     3  |
    |  Saunders     |     2  |
    |  Buffalo      |     3  |
    |  sheridan     |     2  |
    |  Thurston     |     1  |
    |  Dixon        |     3  |
    |  Holt         |     2  |
    |  Kimball      |     1  |
    |  Morrill      |     2  |
    |  Cedar        |     1  |
    |  Keith        |     1  |
    |  Merrick      |     1  |
    |  Hall         |     1  |
    |  Wheeler      |     1  |
    |  Richardson   |     2  |
    |  Nemaha       |     5  |
    |  Frontier     |     1  |
    |---------------+--------|


That's more like it. But it's not in order, so it is sort of bothersome. We can fix that with ordering.


```
sorted_counties = county_totals.order_by('count', reverse=True)
sorted_counties.print_table()
```

    |---------------+--------|
    |  COUNTY       | count  |
    |---------------+--------|
    |  Dawes        |   111  |
    |  Sioux        |    52  |
    |  Sheridan     |    35  |
    |  Cherry       |    30  |
    |  Scotts Bluff |    26  |
    |  Keya Paha    |    20  |
    |  Brown        |    15  |
    |  Rock         |    11  |
    |  Lincoln      |    10  |
    |  Custer       |     8  |
    |  Knox         |     8  |
    |  Banner       |     6  |
    |  Thomas       |     5  |
    |  Dawson       |     5  |
    |  Nemaha       |     5  |
    |  Box Butte    |     4  |
    |  Howard       |     3  |
    |  Dakota       |     3  |
    |  Blaine       |     3  |
    |  Buffalo      |     3  |
    |  Dixon        |     3  |
    |  Douglas      |     2  |
    |  Saunders     |     2  |
    |  sheridan     |     2  |
    |  Holt         |     2  |
    |  Morrill      |     2  |
    |  Richardson   |     2  |
    |  Sarpy        |     1  |
    |  Nance        |     1  |
    |  Platte       |     1  |
    |  Hooker       |     1  |
    |  Polk         |     1  |
    |  Valley       |     1  |
    |  Sherman      |     1  |
    |  Thurston     |     1  |
    |  Kimball      |     1  |
    |  Cedar        |     1  |
    |  Keith        |     1  |
    |  Merrick      |     1  |
    |  Hall         |     1  |
    |  Wheeler      |     1  |
    |  Frontier     |     1  |
    |---------------+--------|


A note on `print_table`: You can limit the number of rows you print by addng max_rows=X to the print_table in the parenthesis, like this:


```
sorted_counties.print_table(max_rows=25)
```

    |---------------+--------|
    |  COUNTY       | count  |
    |---------------+--------|
    |  Dawes        |   111  |
    |  Sioux        |    52  |
    |  Sheridan     |    35  |
    |  Cherry       |    30  |
    |  Scotts Bluff |    26  |
    |  Keya Paha    |    20  |
    |  Brown        |    15  |
    |  Rock         |    11  |
    |  Lincoln      |    10  |
    |  Custer       |     8  |
    |  Knox         |     8  |
    |  Banner       |     6  |
    |  Thomas       |     5  |
    |  Dawson       |     5  |
    |  Nemaha       |     5  |
    |  Box Butte    |     4  |
    |  Howard       |     3  |
    |  Dakota       |     3  |
    |  Blaine       |     3  |
    |  Buffalo      |     3  |
    |  Dixon        |     3  |
    |  Douglas      |     2  |
    |  Saunders     |     2  |
    |  sheridan     |     2  |
    |  Holt         |     2  |
    |  ...          |   ...  |
    |---------------+--------|

Things to note:

* If you're not a Nebraska geography nerd, most of those counties are across the north and northwestern parts of the state in an area called the Pine Ridge.
* Lincoln, the city, is in Lancaster County. According to this data, there have been zero confirmed sightings in Nebraska's second most populous county. Omaha is in Douglas County, with two confirmed sightings.
* Look carefully at Sheridan county. Scan down the list of counties. See any problems?

### Resources for instructors

* Potential assignment: Use local or campus crime data to answer a series of questions. Examples: If you have multiple years of data, how many crimes were reported each year? What is the most common crime type? Which month has the most reported crime?
* Potential assignment: Use salary data from your city or university. Use group by and create the following summaries by job title: count, median and mean. Discuss the differences. For instance, my university salary data includes a very expensive football coach, a moderately expensive basketball coach, and a lot of well paid assistant coaches before we get to chancellors and vice chancellors. How does that affect the numbers?

### Suggested reading

* Jones' [code analyzing crime and temperature data](https://github.com/stlpublicradio/2018-05-31-crime-and-heat-analysis/blob/master/crimes-and-heat.ipynb).
* [Notes on working with big-ish data](https://source.opennews.org/articles/notes-working-big-ish-data/)
