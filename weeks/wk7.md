---
title: Week 7
layout: default
parent: Schedule
nav_order: 7
---

# Week 7 - Nov. 9

**Location** Our Normal Classroom

**Theme** Networks: social, knowledge, and others. Agent Based Models.

**Have Read for Today**
+ Brughmans, Tom. 2010. “Connecting the dots: Towards archaeological network analysis” Oxford Journal of Archaeology, 29:3, 277–303 [link](https://doi.org/10.1111/j.1468-0092.2010.00349.x). Available through our library proxy

+ Mills, Barbara. 2017. “Social Network Analysis in Archaeology”. Annual Review of Anthropology 46:379-397. [link](https://www.annualreviews.org/docserver/fulltext/anthro/46/1/annurev-anthro-102116-041423.pdf?expires=1752075004&id=id&accname=guest&checksum=9CB9F30B21C6A2BA1F9243F7947ECB4D)

+ Romanowska, I., Crabtree, S. A., Harris, K. and Davies, B. 2019: Agent-Based Modeling for Archaeologists: Part 1 of 3. Advances in Archaeological Practice 7 (2). 178–84. [link](https://osf.io/preprints/socarxiv/3gwdn/) (This also comes with a tutorial for the Netlogo language; feel free to read that too if you want)

+ Optional: Graham S, Yates D, El-Roby A, Brousseau C, Ellens J, McDermott C. Relationship Prediction in a Knowledge Graph Embedding Model of the Illicit Antiquities Trade. Advances in Archaeological Practice. 2023;11(2):126-138. [link](https://www-cambridge-org.proxy.library.carleton.ca/core/journals/advances-in-archaeological-practice/article/relationship-prediction-in-a-knowledge-graph-embedding-model-of-the-illicit-antiquities-trade/9B802F4BEFEA325D3221E39BCE4F3A63) The point of sharing this piece with you is to illustrate that there are ways of exploring the latent spaces between the nodes and edges of a network, and that this is a way of surfacing ideas 'hiding' in our knowledge that we didn't initially spot.

**The Plan**
A discussion of how a networked perspective on archaeological data opens up new ways of seeing the past. Then, a further excursion into how archaeological networks can be reanimated. 


**Skill Building**
- We'll build a network of a small farming community from a small rural cemetery
- We'll load a networked representation of the Roman Empire into a Google Colab notebook and calculate some network perspectives on it.
- We'll try to build an agent based model of information (or disease?) diffusion on top of the Roman empire's urban topology

**Homework**
By Friday at noon, have your research compendium for this week complete and in github. You might want to consider the perils of looking at the world through a network lens - and the potentials. Have you encountered this kind of approach in your history classes? What would your other professors make of all this?

![](https://digiarch-2025.netlify.app/docs/support/images/networks/orbis.png)

The [ORBIS geospatial network model of the Roman world](https://orbis.stanford.edu/)

> ORBIS is a multimodal, seasonally variable transportation network model available at orbis.stanford.edu. The model provides for practically unlimited permutations by allowing users to limit modes, change movement cost, and adjust time of year. However, it is as a more simple network that ORBIS can be usefully integrated into other research, such as historical environmental reconstruction or agent-based modeling set in the Roman world. (Scheidel, Weiland and Arcenas 2014)

---

## Historical Cemetery Network Dataset

I'll give you some information I cooked up regarding a small family cemetery. Your goal is to create a new python or R notebook in Google Colab where you load the data in and do some analyzes.

1. take this data, and make a new text file (remember, **you never use Word for something like this**. Use a text editor (and if you don't recall what I mean by that, just ask). Represent the data provided to you below as an 'edgelist' where you list out the relationships. You need to have at least a 'source' and 'target' column, eg:

```csv
source,target
alice,bob
```
You might want to have more columns. When you save the txt file, CHANGE THE FILE EXTENSION to end with .csv, eg: `graveyard_net.csv`. 

Then,

2. make a new python or R notebook
3. load the data in
4. visualize the data
5. determine one or two metrics for the data.

**Hint**
In python, you can load the data with pandas: ```edges_df = pd.read_csv('edges.csv')```

In R, you can load it in with igraph: ```links <- read.csv("edges.csv", header=T, as.is=T)```

Each family seemed to have its own section in the cemetery.

### Thompson Family

<div class="code-example" markdown="1">

| Person | Birth Year | Death Year | Notes |
|--------|------------|------------|-------|
| John Thompson | 1820 | 1889 | Patriarch, miller |
| Mary Thompson | 1823 | 1891 | Wife of John |
| Sarah Thompson | 1847 | 1923 | Eldest daughter |
| Robert Thompson | 1849 | 1901 | Son, took over mill |
| James Thompson | 1851 | 1934 | Youngest son |
| Alice Thompson | 1872 | 1945 | Robert's wife |

</div>

### Hayes Family

<div class="code-example" markdown="1">

| Person | Birth Year | Death Year | Notes |
|--------|------------|------------|-------|
| William Hayes | 1825 | 1895 | Blacksmith, business partner to John |
| Elizabeth Hayes | 1828 | 1901 | Wife of William |
| Thomas Hayes | 1850 | 1918 | Son, continued blacksmithing |
| Margaret Hayes | 1852 | 1925 | Daughter, schoolteacher |
| Robert Thomson and Margaret Hayes | | joint headstone? |
| Catherine Miller | 1875 | 1942 | Daughter, Thomas |
| David Hayes | 1877 | 1950 | Thomas's son |

</div>

### Miller Family

<div class="code-example" markdown="1">

| Person | Birth Year | Death Year | Notes |
|--------|------------|------------|-------|
| Samuel Miller | 1815 | 1882 | Town doctor |
| Ruth Miller | 1818 | 1885 | Wife of Samuel |
| Benjamin Miller | 1845 | 1920 | Son, also doctor |
| Hannah Miller | 1848 | 1929 | Daughter, midwife |
| Edward Miller | 1870 | 1935 | Benjamin's son |
| Catherine Hayes | 1875 | 1942 | Edward's wife |

</div>

### Clark Family

<div class="code-example" markdown="1">

| Person | Birth Year | Death Year | Notes |
|--------|------------|------------|-------|
| Charles Clark | 1830 | 1905 | Store owner |
| Emma Clark | 1833 | 1908 | Wife of Charles |
| Frank Clark | 1855 | 1940 | Son, inherited store |
| Lucy Clark | 1857 | 1932 | Daughter |
| Henry Clark | 1880 | 1955 | Frank's son |
| Rose Clark | 1882 | 1960 | Frank's wife |
| Hannah ... | ? | ? | Frank's first wife? |

</div>

### Wilson Family

<div class="code-example" markdown="1">

| Person | Birth Year | Death Year | Notes |
|--------|------------|------------|-------|
| George Wilson | 1822 | 1890 | Farmer |
| Martha Wilson | 1825 | 1893 | Wife of George |
| Joseph Wilson | 1848 | 1915 | Son, farmer |
| Mary Wilson | 1850 | 1928 | Daughter |
| Peter Wilson | 1875 | 1940 | Joseph's son |
| Anna Wilson | 1878 | 1945 | Joseph's wife |
| Charles Clark and Mary Wilson | | | Joint headstone? |

</div>

## Some code to get you started

If you choose to try this exercise using Python, see if you can work out how to repurpose the code notebook we used to explore ORBIS on your data. If you want to try using R code instead, [here's some starter code](../assets/r_nets).

