# Table of Contents
1. [Clustering](#clustering)
[](#table-of-contents)

[*Back to top*](#table-of-contents)

# Clustering

Clustering makes it possible to group users and items into a specified number of clusters. For finding cluster, there are three different algorithms that can be used:

1. `embedding` with item clusters from the trained machine-learning model and users assigned to the most connected cluster,
2. `plsa`, [Probabilistic Latent Semantic Analysis](https://en.wikipedia.org/wiki/Probabilistic_latent_semantic_analysis) run separately, and
3. `modularity`, network-based [modularity optimization](https://en.wikipedia.org/wiki/Louvain_modularity)run separately.

`embedding` is the fastest method since it uses the trained machine-learning model.

[*Back to top*](#table-of-contents)
