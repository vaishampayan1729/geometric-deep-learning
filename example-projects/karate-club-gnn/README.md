# Karate Club: Graph Neural Networks and Permutation Equivariance

This project explores graph-aware node classification using **PyTorch Geometric (PyG)** and the Karate Club graph. It begins with a fixed neighborhood-aggregation baseline, compares it with Graph Convolutional Networks (GCNs), and introduces experiments motivated by the symmetry principles of Geometric Deep Learning (GDL).

The project is developed as a hands-on companion to the Geometric Deep Learning notebooks in this repository.

## Objectives

The project has three main objectives:

1. **Graph-aware learning:** Investigate how neighborhood information can be used for node classification.
2. **Model comparison:** Compare a fixed neighborhood-aggregation baseline with learned graph-convolutional models.
3. **Permutation equivariance:** Investigate whether model predictions transform consistently when the graph's nodes are relabeled.

The broader aim is to connect practical GNN implementations with the mathematical ideas of graph structure, group actions, and equivariant maps.

## Dataset

We use the `KarateClub` dataset provided by PyTorch Geometric.

The graph contains 34 nodes representing members of a university karate club and their social interactions. PyG provides node features, an edge representation, and a default training mask.

In this notebook, we replace the dataset's original node labels with four randomly assigned synthetic classes. These labels are generated using a fixed random seed to make the experiment reproducible.

**Important:** The synthetic labels do not represent observed nationalities or actual community memberships. Consequently, this version of the project is a demonstration of graph-based classification and model implementation, not a scientifically meaningful experiment in predicting nationality.

## Methods

### 1. Exploratory data analysis

We inspect the graph's node features, edges, labels, and connectivity. NetworkX is used to visualize the graph and display its node labels.

### 2. Train-test split

We construct a stratified train-test split of the nodes, aiming to represent all four classes in both subsets.

The graph remains intact during training and evaluation. This is a **transductive node-classification** setting: the model can use the graph's connectivity and node features, but only training-node labels contribute to the training loss.

Because the graph is small, the resulting test accuracy is sensitive to the particular split and should be interpreted cautiously.

### 3. Fixed neighborhood-aggregation baseline

We first implement a graph-aware baseline directly in PyTorch.

Let \(A\) denote the adjacency matrix and \(X\) the node-feature matrix. We add self-loops and compute the row-normalized adjacency matrix:

$$
\widetilde A=A+I,
\qquad
\widetilde D_{ii}=\sum_j\widetilde A_{ij}.
$$

The aggregated features are

$$
H=\widetilde D^{-1}\widetilde A X.
$$

A trainable linear classifier then produces the class logits:

$$
Z=HW+b.
$$

The neighborhood-aggregation rule is fixed; only the classifier parameters are learned. This baseline provides a simple reference for studying the contribution of learned graph-convolutional representations.

### 4. Graph Convolutional Networks

We subsequently explore GCN models implemented using PyG's `GCNConv` layer. These models learn feature transformations while aggregating information over graph neighborhoods.

The notebook considers architectures with two graph-convolutional layers and a graph-convolutional layer followed by a linear classifier.

The intention is to compare these learned models with the fixed-aggregation baseline under a consistent evaluation protocol.

### 5. Permutation equivariance

A graph's node indices are arbitrary. Relabeling its nodes should not change the underlying graph or the predictions associated with the corresponding nodes.

For a permutation matrix \(P\), the adjacency matrix and node features transform as

$$
A'=PAP^\top,
\qquad X'=PX.
$$

A permutation-equivariant node classifier should satisfy

$$
f(PAP^\top,PX)=P f(A,X).
$$

This is a central mathematical property of message-passing GNNs. A planned extension is to test it numerically by permuting the graph, recomputing predictions, and comparing them after restoring the original node ordering.

### 6. Future directions: Subgraphs and graph minors

Future experiments will investigate how changing the graph domain affects learning.

- **Subgraph-based learning:** Compare learning on the full graph with learning on induced subgraphs, connected regions, or selected neighborhoods.
- **Graph minors:** Explore vertex and edge deletion and edge contraction, investigating how graph simplification changes the available structural information.
- **Structural analysis:** Examine how graph transformations affect neighborhood aggregation, class distributions, and classification performance.

These experiments will require explicit rules for transferring features and labels to transformed graphs and carefully defined evaluation protocols.

## Technology

- Python
- PyTorch
- PyTorch Geometric
- NetworkX
- NumPy
- Pandas
- Matplotlib
- scikit-learn

The notebook is designed to run in Google Colab. A GPU can be used if available, although this small graph does not require one.

## Running the notebook

1. Open `karate_club_gnn.ipynb` in Google Colab.
2. Run the setup cells to install the required libraries.
3. Execute the notebook cells in order.
4. Inspect the graph, class distribution, and train-test split before training the models.
5. Compare the baseline and GCN results, keeping in mind the limitations of the synthetic labels and small test set.

## Scope and limitations

This is an educational and experimental project rather than a benchmark study. The small graph, synthetic labels, and limited number of test nodes constrain what can be concluded from classification accuracy.

The most important learning outcomes are understanding how graph-aware baselines work, implementing GNNs, designing controlled experiments, and connecting permutation equivariance to the mathematical foundations of Geometric Deep Learning.

## References

- [PyTorch Geometric: KarateClub dataset](https://pytorch-geometric.readthedocs.io/en/2.6.0/generated/torch_geometric.datasets.KarateClub.html)
- [PyTorch Geometric: GCNConv](https://pytorch-geometric.readthedocs.io/en/2.6.0/generated/torch_geometric.nn.conv.GCNConv.html)
- Kipf, T. N., and Welling, M. (2017). [Semi-Supervised Classification with Graph Convolutional Networks](https://arxiv.org/abs/1609.02907).
- Bronstein, M. M., Bruna, J., Cohen, T., and Veličković, P. [Geometric Deep Learning: Grids, Groups, Graphs, Geodesics, and Gauges](https://arxiv.org/abs/2104.13478).