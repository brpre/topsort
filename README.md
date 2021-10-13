# topsort
making sources of information more accessible by finding and ordering prerequisite knowledge.

Strategy:
0. Scrape a given page on simple wikipedia for related items, keywords, links to other articles, etc (ideally generalize to other sources, but use this as a starting point) make sure that this is depth limited search and that we're looking for prerequisite knowledge, so a page is found to be successful if it references the topic of or a parent topic of the query page. Here's a rough potential algo for this:
  a. for each linked candidate keyword/topic found, search the page for instances of our term being used (maybe narrow scope to just links/tags for efficiency using bs4, don't just scan plaintext fo an entire webpage). If the candidate has at least once reference to the query term, naively put it in the "worth investigating, make it a node" pile.
  b. for each candidate in the node pile, get a list of its neighbors (a neighbor is a page linked directly to/from a given page, edges will be directed but some edges go both ways. could be done partially in the above step.)
1. clean/format the scraped data into a json file that neo4j or some other graph representation can interpret/use. make sure that nodes have the correct labels and that they have lists of neighbors that aren't super long, maybe naively prioritize number of instances or cut out terms that don't relate back, I'm not sure.
2. run an algo that checks if the graph is a DAG (Most likely won't be because of things that reference each other). maybe just find cycles and then try to predict which item is upstream/parent to the other by some mechanism. NLP? idk man
3. Once we have a graph with generally clean edges, ideally a DAG, we can run a topological sorting algorithm on it to figure out which knowledge is upstream of our query.
4. Make a cool visualization with seaborn/neo4j/something that allows links being attached to nodes. Provide an ordered list of prereq reading, and a list of potentially interesting follow up reads that were discovered in the process

The above algo is subject to change, of course. Hopefully a decent, albeit naive and difficult, starting point. Don't forget to simplify and add lightness
