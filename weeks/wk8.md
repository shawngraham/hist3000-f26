---
title: Week 8
layout: default
parent: Schedule
nav_order: 8
---

# Week 8 - Nov. 9

**Location** Our classroom

**Theme** Practical Necromancy... erm, artificial neural networks (yes, the things that everyone now calls 'ai')

**Have Read for Today**
- Perry S. The Enchantment of the Archaeological Record. European Journal of Archaeology. 2019;22(3):354-371. doi:10.1017/eaa.2019.24 [link](https://www-cambridge-org.proxy.library.carleton.ca/core/journals/european-journal-of-archaeology/article/enchantment-of-the-archaeological-record/6B71DCDB28D3FABE22660EEA860ED7FE)
- Huggett, J. (2022). ‘Is Less More? Slow Data and Datafication in Archaeology’. In K. Garstki (Ed.), Critical Archaeology in the Digital Age. UCLA Cotsen Institute of Archaeology Press. pp. 97–110. [link](https://escholarship.org/uc/item/0vh9t9jq#page=112) (scroll to chapter 6 if that link doesn’t quite take you there)
- Magnani, Matthew, and Jon Clindaniel. “Artificial Intelligence and the Interpretation of the Past.” Advances in Archaeological Practice 14, no. 2 (2026): 218–33. [link](https://doi-org.proxy.library.carleton.ca/10.1017/aap.2025.10110). 
- Optional: A complete free book on archaeology, history, and AI by me. [link](https://thedigitalpress.org/practical-necromancy-for-beginners/), to have handy should you want it.

**The Plan**
I'll talk about how we got to now with regard to 'ai', versus the much longer use of computers in archaeology that has gone under a variety of names; in particular I want to talk about machine learning in archaeology. We'll take a look at this: [Aeneas, Predicting the Past](https://predictingthepast.com/aeneas) too. And I'll talk about how we used these techniques in our project looking at the online trade in human remains, and our project looking at climbing culture on Mount Everest.


**Skill Building**
- We're going to build a very stupid language model from scratch that knows about archaeology ([using this notebook ported into Colab](https://github.com/shawngraham/pn_notebooks/blob/main/1_hands_on_1_flinders_petrie.ipynb)). 
- We'll build an image classifier ( first using [this](https://teachablemachine.withgoogle.com/), and then [using this](https://github.com/shawngraham/pn_notebooks/blob/main/2_experiment_2_Use_ArchaeoCLIP_in_a_notebook.ipynb). Note there are some interesting differences between how these work, why they work, and we'll talk about what that might mean for doing digital archaeology.)
- Finally, and this is only for those people who want to push things, what if we had a word calculator that could match our free-text queries about archaeological data to the exact appropriate data? I'm imagining the way the crew of the Enterprise:TNG 'analyze' data by asking the machine questions. [Here's a computational notebook](https://colab.research.google.com/drive/1XNFBcEb7qbYK-soNmyfSwjDR94n0ROIh?usp=sharing) that uses a small LLM as a query layer on top of some fictitious data from an excavation. It does this by 'embedding' the data into the space of language that it 'knows'. Then, when you query, it similarly embeds your query into that space. Then it measures the position of your query against the positions of your data, grabs the closest material, and uses its understanding of language to generate a response to answer the query with the data. (One problem with this: is it true that the closest most similar data point to a query is the same thing as an 'answer'?)

**Homework**
By Friday at noon, have your materials for this week complete and in github. Think about the ethical issues that these approaches might raise, the questions of labour. Think about the friction you encounter using these. 
