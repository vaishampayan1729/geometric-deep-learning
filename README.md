# Geometric Deep Learning

A computational laboratory for exploring `Geometric Deep Learning (GDL)` through examples, implementations, and experiments.

This repository accompanies my study of:

> Michael M. Bronstein, Joan Bruna, Taco Cohen, and Petar Veličković,  
> **Geometric Deep Learning: Grids, Groups, Graphs, Geodesics, and Gauges**  
> [arXiv:2104.13478](https://arxiv.org/abs/2104.13478)

together with useful references.

The repository is organized according to the sections of the GDL proto-book.

## Purpose

The goal of this project is to supplement the mathematical development of the
GDL proto-book with computational exploration.

For each section, the corresponding Jupyter notebook may contain:

- coding examples;
- mathematical examples and non-examples;
- visualizations;
- computational experiments;
- implementations of ideas introduced in the proto-book;
- experiments extending or testing those ideas;
- additional references and related literature;
- observations and questions that arise while studying the material.

The notebooks are therefore not intended to reproduce the proto-book.
Instead, they provide a computational laboratory in which its ideas can be
explored and tested.

## Learning through examples and experiments

A central principle of this project is that mathematical ideas should be
explored computationally whenever possible.

The general workflow is:

    mathematical idea
          ↓
       example
          ↓
     implementation
          ↓
      experiment
          ↓
      observation
          ↓
    further questions

The experiments may sometimes confirm an expected mathematical property,
while in other cases they may reveal subtleties, limitations, or interesting
questions that are not immediately apparent from the formal definition.

## Organization

The notebooks follow the structure of the GDL proto-book, but build the prerequisites
whenever needed:

```text
notebooks/
├── 01_sets_and_map.ipynb
├── 02_groups.ipynb
├── 03_linear_spaces.ipynb
├── 04_learning_in_high_dimension.ipynb
├── 05_geometric_priors-i.ipynb
├── 06_functional_analysis.ipynb
├── 07_fourier_analysis.ipynb
├── 08_wavelets_and_multiscale_signal_processing.ipynb
├── 09_geometric_priors-ii.ipynb
├── 10_pytorch_geometric_tutorial.ipynb
└── 11_graph_theory_fundamentals.ipynb


```

The notebooks will be developed nonlinearly. For example, an experiment
motivated by a later section may lead to additions to an earlier notebook.

References relevant to a particular topic will be included directly in the corresponding notebook
rather than maintained in a separate bibliography.

## Computational environment

The experiments are written primarily in Python and developed using Jupyter
notebooks.

The project uses a dedicated conda environment and Jupyter kernel named:

gdl

The environment includes, among other packages:

- PyTorch
- PyTorch Geometric
- NetworkX
- SymPy
- Geomstats
- e3nn
- GUDHI
- TopoNetX
- TopoModelX

The exact set of dependencies will evolve as the project develops.

## Project structure
```text
geometric-deep-learning/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── notebooks/
│   └── Section notebooks
│
├── code/
│   └── Reusable implementations
│
└── figures/
    └── Figures used across notebooks
```
The notebooks are the primary component of the project.

The code/ directory will contain reusable implementations when they emerge
naturally from the experiments. The figures/ directory is reserved for
figures that are useful outside an individual notebook.

## Status

This is an ongoing project.

The current work follows my progress through the GDL proto-book. New examples,
experiments, implementations, observations, and references will be added
progressively.

The repository is intended to evolve alongside the study of Geometric Deep
Learning.
