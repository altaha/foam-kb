# Graph Representation Learning

Graphs: General language to represent complex systems.

ML tasks on Graphs:
- Node Classifcation
- Link Prediction
- Community Detection (like clustering)
- Network similarity (similar to unsupervised learning)

The IID assumption does not usually hold on graph data because of the connections.

Node Classifcation
- Example: Is this node a real person or a bot?
- Example: Classifying proteins

Link Prediction
- We are uncertain about if edges exist between existing nodes
- Example: Content recommendation is Link Prediction
    - A bipartite graph of users and items. Predict missing edges.

**Missed a bit between 12pm and 1205pm**

## Node Embeddings
Need:
- an Encoding function
- A node similarity function
- And approximate similarity with embedding dot product

Encoding:
- Shallow encoding: embed nodes as columns in a matrix.

Similarity:
- Siimple adjacency: nodes have edges between them
- Random Walk embeddings: nodes are connected by random walks in the graph (can extend beyond immediate adjacency)

## Graph Neural Networks
From Shallow to Deep encoders


