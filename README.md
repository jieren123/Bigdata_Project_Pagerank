## Project Overview 
In this project, by using the **Hadoop MapReduce framework** to calculate each Wikipedia pages, produce an ordered list of page titles, along with their ranks. Moreover, this project prevents **dead-ends** and **spider-traps** suitiation by corporating the factor β into matrix by multiplying each of its elements by 0.2.

## Pagerank Output Visualization  
After iterated three times, I selected Page ID =6 as an example (black point). This shows the pagerank value of selected page relative to other pages. 
![alt text](https://github.com/jieren123/Bigdata_Project_Pagerank/blob/master/Diagrams/Page-rank-No.6page.gif
 "Page Rank")

## Dataset Description: 
- transition.txt has the following format: `to1 from1 from2 from3 from4......` where `to1` is an interger labelling a page link to and
where `from1` is an integer labelling a page that has links from, separating by '\t'.
- pr.txt has the following format: `page_id prob` where page_id is ID of the page and prob is probaility of each page, separating by '\t'.

## PageRank Alogrithm
PageRank is a calculation evaluates the quality and quantity of links to a webpage to determine a relatvie score of that page's importantce and authority. This project proposes a generalization of the PageRank aglorithm based on both out-links and in-links by using a iterative algorithm as an alternative interpretation of the matrix based techniques Also the PageRank algorithm can specify a probability at any step that a person will continue clicking outgoing links.
 ![alt text](https://github.com/jieren123/Bigdata_Project_Pagerank/blob/master/Diagrams/pagerank.png "page_rank")

## Dead-ends & Spider-traps Explains 
- A group of pages is a **spider-trap** if there are no links from within the group to outside the group.
 ![alt text](https://github.com/jieren123/Bigdata_Project_Pagerank/blob/master/Diagrams/one_node_spider_trap.png "spider_traps")

- Pages with no outlinks are **dead-ends** for the random surfer 
 ![alt text](https://github.com/jieren123/Bigdata_Project_Pagerank/blob/master/Diagrams/two_levels_dead_ends.png "dead-end")

## Main Files: 
- UnitMultiplicaiton.java: This class is the mapper class. It takes an input file which has graph data in form of node and its adjacency lists and generates files containing nodes, their page ranks and their adjacency lists. Finally emit a key value pair of (page-id,prob)

- UnitSum.java: This class is the reducer class. It receives a key: page-id and a list of its values: probabilities. For each value in the list If it is a node, the initialize the node with this node. Else if it a pagerank value sum it up and set the pagerank by its convergence value into the list. 

- Driver.java

## Architecture Overview Diagram



## Compiling and Running
```
hadoop com.sun.tools.javac.Main *.java  
jar cf pr.jar *.class 
hadoop jar pr.jar Driver /transition /pagerank /output 3 #3: iterate three times
```

## Output
```
#args0: dir of transition.txt
#args1: dir of PageRank.txt
#args2: dir of unitMultiplication result
#args3: times of convergence（make sure the code run successfully when args3=1, then test args3=40）
```

## Reference 
- [The PageRank Citation Ranking:Bringing Order to the Web](http://ilpubs.stanford.edu:8090/422/1/1999-66.pdf)
- [Convergence Analysis Of An Improved Pagerank Algorithm](https://projects.ncsu.edu/crsc/reports/ftp/pdf/crsc-tr04-02.pdf)
