# Sorting

### Sorting Algorithms

There are numerous sorting algorithms that, over time, have become part of the computer science lexicon.

Building on the discussion of Complexity from the previous chapter, we will look at several of the more popular algorithms and their performace given a collection of 'n' items.

#### Selection Sort
Average Case: n² <br/>
Worst Case: n²

#### Insertion Sort
Average Case: n² <br/>
Worst Case: n²


#### Bubble Sort
Average Case: n² <br/>
Worst Case: n²


#### Quick Sort
Average Case: n*log(n) <br/>
Worst Case: n²


#### Merge Sort
Average Case: n*log(n) <br/>
Worst Case: n*log(n)


There are countless resources available for more information on each of these sorting algorithms. For instance, [Wikipedia](https://en.wikipedia.org/wiki/Sorting_algorithm) is a good starting point.


### Why sort at all?

Are there scenarios when sorting doesn't make sense? Or isn't worth the cost/time?

![Ticketmaster](images/ticketmaster.jpg "Ticketmaster" | width=300)

![Kickstarter](images/kickstarter.png "Kickstarter" | width=300)


### When do we need to sort?

If we imagine a collection of items that we are continuously adding to, then the intuitive approach is to insert the time "where it belongs" -- that is, at the time of insertion. But this is not the only option.

Every application has its own unique set of circumstances. And it's important to understand the moments in the application flow where high-performance is a priority, and if there are other moments where less than optimal may be acceptable.

Imagine a system that inserts new records into a collection (at the rate of dozens per minute). And then at the end of each month, a task is run that creates a report summary for this previous month's additions. Given this scenario, is it worth the effort to maintain the sorted collection with every new insert? Seeing as we will only query the collection once per month (to generate the report summary), sorting the collection as part of that task seems a better strategy.

#### We could sort a list at ... Insertion, Deletion, Retrieval, Query... or perhaps even some task that is scheduled to run arbitrarily.