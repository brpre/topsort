# Optimized Learning with Topologically Sorted Knowledge Graphs
a fancy name for a simple problem: making sources of information more intellectually accessible by finding and ordering the prerequisite knowledge you need to understand what you're looking at

Have you ever been curious about a topic (or had to learn something for a class or work) and found that your lack of domain knowledge made it extremely difficult to find a good starting point? When it seems like every resource out there is full of complicated concepts and vocab, even wikipedia, it can feel like you're never going to understand the topic. **My goal with this project is to increase the accessibility of complex information by finding and ordering prerequisite knowledge for a given source, starting with Wikipedia pages.** My approach is to collect linked references from a given Wiki page, try to convert the corresponding graph into a directed acyclic graph (a DAG), and then topologically sorts graph to generate an ordered list of resources and topics that will help build a foundation for the topic at hand.

One of my main motivations for this project is trying to read academic research papers on cool topics and experiencing a crushing sense of inadequacy when I have no idea what's going on in a paper. My next goal with this project is to extend the work with Wiki pages to papers posted on [arxiv.org](https://arxiv.org) with the goal is generating guided literature surveys 
· Currently working to improve accessibility of academic research fields by generating an overview of previously published work on the topic to support the reader. Such overviews are often called [literature reviews](https://en.wikipedia.org/wiki/Literature_review).


Strategy:
1. **Scrape a given page on simple wikipedia for related items, keywords, links to other articles, etc. Make sure that this is depth limited search and that we're looking for prerequisite knowledge, so a page is found to be successful if it references the topic of or a parent topic of the query page.** 
  a. rough algo: for each linked candidate keyword/topic found, search the page for instances of our term being used (maybe narrow scope to just links/tags for efficiency using bs4, don't just scan plaintext fo an entire webpage). If the candidate has at least once reference to the query term, naively put it in the "worth investigating, make it a node" pile.
2. **clean/format the scraped data into a json file that neo4j can interpret/use.** make sure that nodes have the correct labels and that they have lists of neighbors that aren't super long, maybe naively prioritize number of instances or cut out terms that don't relate back, I'm not sure.
3. Convert the graph into a directed acyclic graph: find pages that reference each other create cycles, resolve cycles by determining which page is upstream/parent to the other by some mechanism, maybe num times each page references each other, page cardinality, or something else, just try something and see if it works
4. Once we have a graph with generally clean edges, ideally a DAG, we can run a topological sorting algorithm on it to figure out which knowledge is upstream of our query.
5. Provide an ordered list of prereq reading, and a list of potentially interesting follow up reads that were discovered in the process
6. Make a cool visualization with neo4j and/or seaborn that serves as a human-readable output - a visually topologically sorted graph where each node is a wiki page with an attached link. 

The above algo is subject to change as this project develops further. Hopefully a decent starting point. 

simplify and add lightness