---
layout: default
title: loiselle
nav_exclude: true
---

```R
# Hope Loiselle's Code
# your task: annotate it with what you think
# she's trying to do; and compare it with
# Marwick's original paper: what aspect of his analysis
# does this bit of code address, and do your findings
# match up with his?
library(curl)
library(stringr)
library(dplyr)
library(tidyr)

library(tidyverse)
flakes_TL <- read.csv(curl("https://raw.githubusercontent.com/benmarwick/teaching-replication-in-archaeology/refs/heads/master/analysis/supplementary-materials/submitted-assigments/Hope-Loiselle/Tham_Lod_Area_1_lithics-1.csv"), header = TRUE )
flakes_BR <- read.csv(curl("https://raw.githubusercontent.com/benmarwick/teaching-replication-in-archaeology/refs/heads/master/analysis/supplementary-materials/submitted-assigments/Hope-Loiselle/Ban_Rai_Area_3_lithics-1.csv"), header = TRUE) 

##- new cell

# dorsal cortex and dorsal scars
TL_dorsal <-
  flakes_TL %>%
  select(DORSAL_COR, DORSAL_SCA, SITE, EXCAVATION)

BR_dorsal <-
  flakes_BR %>%
  select(DORSAL_COR, DORSAL_SCA, SITE, EXCAVATION)

TL_BR_dorsal <- bind_rows(TL_dorsal, BR_dorsal)

##- new cell

ggplot(TL_BR_dorsal, aes(SITE, DORSAL_COR)) +
  geom_boxplot()

dorsal_cortex_proportion <-
  TL_BR_dorsal %>%
  group_by(SITE, EXCAVATION, DORSAL_COR) %>%
  tally() %>%
  mutate(DORSAL_COR = ifelse(DORSAL_COR == 0, "zero", "not zero")) %>%
  group_by(SITE, EXCAVATION, DORSAL_COR) %>%
  tally() %>%
  filter(!is.na(DORSAL_COR)) %>%
  spread(DORSAL_COR, n) %>%
  mutate(dorsal_proportion = zero / (`not zero` + zero))

ggplot(dorsal_cortex_proportion, aes(SITE, dorsal_proportion)) +
  geom_boxplot()
 ```

Having done that, read Loiselle’s conclusion (available in the repository [here](https://github.com/benmarwick/teaching-replication-in-archaeology/blob/master/analysis/supplementary-materials/submitted-assigments/Hope-Loiselle/Loiselle_Replication_Report_Lithics.docx); it’s in Word format, so hit the ‘download’ icon to grab it then open it in Word).

Compare your results with Loiselle’s work and Marwick’s paper. Do you think his conclusion stands up? How about Loiselle’s?