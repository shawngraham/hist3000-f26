---
layout: default
title: ads
nav_exclude: true
---

## Explore the Archaeology Data Service

Set up a new Colab notebook and make sure the runtime is set to use the R kernel. Copy the script below into your notebook file in your workbench, breaking it into individual cells. Work through it one line at a time, taking note of the comments as you go. When you get to the end, explore the ADS, find another dataset, and try modifiying the code to explore the new data. What kind of work do you imagine must be necessary to get data into shape for the ADS? What kinds of decisions need to be made? You might want to consider how “[The Numbers Don’t Speak For Themselves](https://mitpressonpubpub.mitpress.mit.edu/pub/6ui5n4vo/release/4?readingCollection=09555901)” as you think about that.

Any data published as CSV files with the ADS can be pulled into R for exploration, asking your own questions with it, and generally doing research. Our example uses the data from Ewan Campbell’s 2007 deposit “Imported Material in Atlantic Britain and Ireland c.AD400-800”, found at [http://archaeologydataservice.ac.uk/archives/view/campbell_cba_2007/downloads.cfm](http://archaeologydataservice.ac.uk/archives/view/campbell_cba_2007/downloads.cfm). What interesting questions can you ask?

```R
# set up required libraries
library(curl)
library(stringr)
library(dplyr)

#--- new cell!

#start by reading in Campbell's table of glass artefacts and printing it out

# we load it up from the web, and make the ID number the row numbrer
glass <- read.csv(curl("http://ads.ahds.ac.uk/catalogue/adsdata/arch-788-1/dissemination/csv/imports_database/Glass.csv"), header = TRUE, row.names="ID")

### NB!!! When you run this line, you'll get an error. Why? The ADS changed its URL patterns!!!

#--- put this next bit into a new cell!

# After some exploring, I find that you can change the URL like so:

glass <- read.csv(curl("https://archaeologydataservice.ac.uk/archiveDS/archiveDownload?t=arch-788-1/dissemination/csv/imports_database/Glass.csv"), header = TRUE, row.names="ID")

# so word to the wise - you might find broken links on the ADS website, where you need to change
# http://ads.ahds.ac.uk/catalogue/adsdata/
# for
# https://archaeologydataservice.ac.uk/archiveDS/archiveDownload?=

#--- new cell!
# view the data
View(glass)

#--- new cell!
# Get all the finds from the table where the "Form" is "Cone Beaker"
# We create a new object 'ConeBeakers', which gets 'glass' filtered on the 'Form' column for the phrase 'Cone beaker'
# '<-' passes the results from the operations on its right to the object on its left
# '%>% pipes the object on its left to the commands on its right
ConeBeakers <- glass %>%
  filter(str_detect(Form, "Cone beaker"))

# Want a different vessel form? Just copy those two lines above,
# paste them after this comment block, and change "Cone beaker" to something
# else you see in the table 'glass'.

#--- new cell!
# double check you've got the stuff you want, eg:
ConeBeakers

#--- new cell!
# Now you can start to explore. Which sites have most of the Cone beakers?
# Make a bar plot of how often each site appears in the Cone Beaker table.

# first we use the 'table' command to count up the number of times each site appears
siteCounts <- table(ConeBeakers$Site)

# then we sort the list
siteCounts <- sort(siteCounts, decreasing=TRUE)

# check
siteCounts

#--- new cell!

# barplot(data, title, label, show labels, make 'em really small)
barplot(siteCounts, main="Sites", xlab="Site", las=2, cex.names=.5 )

#--- new cell!
# Now you do it for a different vessel form.

#--- new cell!
# Whithorn has a lot of Cone Beakers. I wonder what else is there?
# We can follow the same pattern as when we searched for cone beakers,
# but searching the 'site' column instead from our original 'glass' data.

Whithorn <- glass %>%
  filter(str_detect(Site, "WHITHORN"))

View(Whithorn)

#--- new cell!
# and now we make a barplot for the other kinds of forms at that site

whithornCounts <- table(Whithorn$Form)
whithornCounts <- sort(whithornCounts, decreasing=TRUE)
barplot(whithornCounts, main="Fomrs", xlab="Form", las=2, cex.names=.5)

# you get the idea. Where it says `cex.names` we're adjusting the size of the font for the 'names' variable. 
# Earlier in the course, I showed you some basic stats with R.
# Try doing that on this data.

crosstab <- xtabs(~Form+Group, Whithorn)
crosstab
barplot(crosstab, las=2)

#--- new cell!
#----
# Explore ADS: can you find an interesting dataset and get it loaded into R?
#----
```