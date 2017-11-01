# Software Design Concerns


## Maslow's Hierarchy

Software development takes the academic ideas of computer science and applies them
to the realities of working with various browsers, devices, and human beings in the 
context of an organization.

As a seasoned developer, one of the key things that you will realize is that there 
are a *pattern of problems* that are encountered when building software, which can
be grouped and prioritized as follows.

![Design Concerns Hierarchy](images/concerns.png "The hierarchy of design concerns.")


### Correctness

These are the issues that your QA will nail you on.  The application doesn't function as
per specification.  These are fairly obvious, except in the case of false positives or 
timing / threading issues which can be extremely painful to trace.

Some examples of this would be:
- An application crashes when a form is submitted with invalid or missing data.
- A button navigates to the wrong page.
- Sometimes a data gets lost.


### Scalability

These are the next tier of problems.  The application functions correctly, but that is
without considering the constraints of space and time.

Some operations in an application can't take forever to execute, and as the data scales
they might even take longer to process.  Other operations require a lot of memory, which 
even on a desktop has a limit.

Some examples of this would be:
- You have to display a list of items from a potentially large data set (e.g. Tweets).
- You have to parse large data sets (e.g. full resolution images or large documents).
- You have to make HTML DOM updates across the whole document root AND the web page could 
be very large.
- You create an animation framework.


### Maintainability

These problems are the ones that typically take grey hairs to figure out.  They surface as
you consider the nuances of teams of developers working together over as a codebase evolves:
- New technologies surface and old technologies become deprecated.
- Applications grow in features and teams start to break out into more focused groups.
- User experience is redesigned.
- Developers leave and new ones come on board.


