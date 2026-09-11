---
layout: default
title: r_nets
nav_exclude: true
---

In colab, change the runtime to use R. Drag and drop your data into the file tray. Then use the code below to get you started. **Do not just dump this all into a single block**. Try to maintain one block = one main operation. And then use text blocks between the code blocks to keep track of your thoughts etc.

```R
# install igraph; this might take a long time
# you only run this line the first time you install igraph:
install.packages('igraph')
# a lot of stuff gets downloaded and installed.
# 
# now tell RStudio you want to use the igraph pacakge and its functions:
library('igraph')

# now let's load up the data by putting the csv files into nodes and links.
# we're keeping the first row as a 'header'

nodes <- read.csv("nodes.csv", header=T, as.is=T)
links <- read.csv("edges.csv", header=T, as.is=T)
#examine data
head(nodes)
head(links)

#we are going to tell igraph that the network is directed, that the relationship Alice to Bob is different than Bob's to Alice. This isn't always a critical distinction to make and depends on your dataset.
#AND - we're going to do this just from the edge data
#Create network from edges only - igraph will infer the nodes
net <- graph_from_data_frame(d=links, directed=T)

#(if we wanted to include the node data specifically, we could do this:
# net <- graph_from_data_frame(d=links, vertices=nodes, directed=T)
# see the difference?
# Calculate closeness centrality
closeness_cent <- closeness(net, normalized = TRUE)

# Histogram
hist(closeness_cent, 
     breaks = 20,
     main = "Distribution of Closeness Centrality",
     xlab = "Closeness Centrality",
     ylab = "Frequency",
     col = "lightgreen",
     border = "white")
abline(v = mean(closeness_cent), col = "red", lwd = 2, lty = 2)

# Network plot colored by closeness
close_colors <- colorRampPalette(c("lightblue", "darkgreen"))(100)
V(net)$color <- close_colors[as.numeric(cut(closeness_cent, breaks = 100))]

plot(net, 
     layout = layout_with_fr,
     vertex.size = closeness_cent * 50 + 5,  # Scale by closeness
     vertex.color = V(net)$color,
     vertex.frame.color = "white",
     edge.color = "gray50",
     edge.arrow.size = 0.5,
     vertex.label = NA,
     main = "Network: Closeness Centrality")

# Calculate betweenness centrality
betweenness_cent <- betweenness(net, normalized = TRUE)

# Histogram
hist(betweenness_cent, 
     breaks = 20,
     main = "Distribution of Betweenness Centrality",
     xlab = "Betweenness Centrality",
     ylab = "Frequency",
     col = "orange",
     border = "white")
abline(v = mean(betweenness_cent), col = "red", lwd = 2, lty = 2)

# Network plot colored by betweenness
between_colors <- colorRampPalette(c("lightblue", "darkorange"))(100)
V(net)$color <- between_colors[as.numeric(cut(betweenness_cent, breaks = 100))]

plot(net, 
     layout = layout_with_fr,
     vertex.size = sqrt(betweenness_cent) * 10 + 5,  # Square root scaling
     vertex.color = V(net)$color,
     vertex.frame.color = "white",
     edge.color = "gray50",
     edge.arrow.size = 0.5,
     vertex.label = NA,
     main = "Network: Betweenness Centrality")
# Detect communities using modularity
communities <- cluster_louvain(as.undirected(net))  # Convert to undirected for community detection
modularity_score <- modularity(communities)

# Print modularity score
cat("Modularity score:", modularity_score, "\n")
cat("Number of communities:", length(communities), "\n")

# Histogram of community sizes
community_sizes <- sizes(communities)
hist(community_sizes, 
     breaks = 10,
     main = paste("Distribution of Community Sizes\nModularity =", round(modularity_score, 3)),
     xlab = "Community Size",
     ylab = "Frequency",
     col = "purple",
     border = "white")

# Network plot colored by community
community_colors <- rainbow(length(communities))
V(net)$color <- community_colors[membership(communities)]

plot(net, 
     layout = layout_with_fr,
     vertex.size = 8,
     vertex.color = V(net)$color,
     vertex.frame.color = "white",
     edge.color = "gray50",
     edge.arrow.size = 0.5,
     vertex.label = NA,
     main = paste("Network: Communities (Modularity =", round(modularity_score, 3), ")"))
```