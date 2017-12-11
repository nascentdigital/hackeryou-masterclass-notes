
# Searching




## Linear Search
For the previous section of the contacts list, say you wanted to find 'Amy' within the list of length 8. What would be an approach to look for that object in an array?

One approach is using Linear Search, starting from the first element in the array, we iterate to the next element to check if it is the element with the first name 'Amy'. We continue until we find the element that matches our criteria. 

For more details on Linear Search, check out [Linear Search](http://www.geeksforgeeks.org/linear-search/)

So how many operations did that take?
Given our array list of  
**[ Fry, Leela, Bender, Professor, Amy, Zapp, Hermes, Zoidberg]** 
, using Linear Search approach, it would take 5 iterations to find Amy.

How many iterations will it take to find Fry? Zoidberg?

With what we can deduce from this quick example. We can determine that the number of iterations to find what we need through Linear Search has the relation of *n* elements of the array = *n* operations. We represent this with Big-O notation: O(n)

![Image of O n](/images/o_n.png)

10 contacts VS 1,000,000 contacts
### Find Amy in the ContactsList

## Understanding Performance and Complexity
