# Sudoku Solver with Genetic Algorithm and Graph Coloring

This repository presents an approach to solving Sudoku puzzles using genetic algorithm and graph coloring. The proposed algorithm represents Sudoku puzzles as graphs and employs graph coloring to solve them. The genetic algorithm is used to find the optimal graph coloring solution. The genetic algorithm described here utilizes more than one parent selection and mutation methods on a randomized basis. This results in shifting the solution to the global optimum more quickly than using a single-parent selection or mutation method. The proposed algorithm succeeded at solving the sample Sudoku successfully.

## Abstract

This research paper proposes an approach to solving Sudoku puzzles using genetic algorithm and graph coloring. The proposed algorithm represents Sudoku puzzles as graphs and uses graph coloring to solve them. The genetic algorithm is used to find the optimal graph coloring solution. The genetic algorithm described here utilizes more than one parent selection and mutation methods on a randomized basis. This results in shifting the solution to the global optimum more quickly than using a single-parent selection or mutation method. The proposed algorithm succeeded at solving the sample Sudoku successfully.

## Index Terms

- Genetic algorithms
- Graph Coloring
- Randomized methods
- Chromatic Number

## Introduction

The Graph Coloring Problem (GCP) is a well-known problem in computer science that is considered difficult to solve efficiently. The problem involves coloring the vertices of aconnected graph in such a way that no two adjacent vertices
have the same color. The goal is to use as few colors as possible to achieve this. This minimum number of colors
required is known as the Chromatic Number (χ(G)) of the graph. While edge coloring is also a part of graph coloring,
but the term graph coloring usually refers to vertex coloring.

χ(G) = min k : P (G, k) > 0 (1)

![color](https://github.com/SamarpreetSingh/Sudoku-Solver-with-Graph-Coloring-using-Genetic-Algorithm/assets/56433539/d867c7c7-c168-425f-ba63-9870928a20f6)

The problem is NP-complete, meaning that there is no known algorithm to solve it in polynomial time. Graph col-
oring has practical applications in scheduling, map coloring, register allocation, sudoku and many other fields. Despite its
practical significance, the GCP is known to be computationally challenging due to its combinatorial nature and non-linear
constraints.

Various heuristics and metaheuristics have been proposed
in the literature to tackle the GCP, including exact algorithms,
greedy algorithms, simulated annealing, tabu search, and ge-
netic algorithms. Genetic algorithms (GAs) are a class of
population-based search algorithms inspired by the principles
of natural selection and genetics. GAs have been widely
applied to various optimization problems due to their ability
to handle complex search spaces, maintain diversity in the
population, and provide near-optimal solutions in a reasonable
amount of time.
In this paper, we propose a GA-based approach [5] for
solving the GCP. The proposed GA utilizes an integer encod-
ing scheme to represent the solutions and employs a fitness
function that considers the number of adjacent vertices of
the graph having the same color. The GA also incorporates
various genetic operators such as crossover, and mutation, to
generate new candidate solutions and maintain diversity in the
population.
The rest of the paper is organized as follows: Section 2
provides a brief overview of the related work on the GCP [4]
and genetic algorithms. Section 3 & 4 describes the proposed
GA-based approach in detail and also explains how we are
converting solving sudoku to GCP, including the encoding
scheme, fitness function, and genetic operators. Section 5
presents the experimental results. Finally, Section 6 concludes
the paper and discusses future directions of research

## Literature Review

Theoretical elements of the Graph Colouring Problem have been extensively studied in the context of its generalization as a Constraint Satisfaction Problem. Various techniques were presented in the past. Musa et al.[1] presented a hybrid technique for solving the Graph Coloring Problem where a genetic algorithm along with the Wisdom of Artificial Crowds was used. 
Raktim et al.[3] used an optimized backtrack algorithm to solve Combinatorial problems like Sudoku.
None of these methods have applied graph coloring using the genetic algorithm on sudoku.

## Problem Formulation
The following section will discuss the problem formulation for the Graph Coloring Problem (GCP):

### Inputs
The input of the problem is a sudoku of dimension 9 x 9. We are representing this sudoku in the form of a graph using an adjacency matrix of dimension 81 x 81.

### Adjacency Matrix
An adjacency matrix allows representing a graph with a V × V matrix `Adj = [Adj(i, j)]` where each element `Adj(i, j)` contains the attributes of the edge (i, j). 

![Example Graph and its adjacency Matrix](https://github.com/SamarpreetSingh/Sudoku-Solver-with-Graph-Coloring-using-Genetic-Algorithm/assets/56433539/d903de4f-0a22-4200-b620-bf3d34501c90)
![m2](https://github.com/SamarpreetSingh/Sudoku-Solver-with-Graph-Coloring-using-Genetic-Algorithm/assets/56433539/190cfd68-8066-404b-b62b-08fd74c4efa3)


### Rules of Sudoku
Sudoku is played on a 9x9 grid, divided into nine 3x3 squares. The sudoku contains certain filled cells and the empty cells are filled according to the following rules:
- Every row must contain unique numbers from 1 to 9
- Every column must contain unique numbers from 1 to 9
- Every 3x3 block must contain unique numbers from 1 to 9

### Adjacency list formulation
The adjacency list is formulated according to the above rules of sudoku. In GCP, all connected nodes of the graph must be assigned different colors. So we create an edge for all the cells of a row, all the cells of columns, and all the cells in a 3x3 block.

![Example Graph and its adjacency List](https://github.com/SamarpreetSingh/Sudoku-Solver-with-Graph-Coloring-using-Genetic-Algorithm/assets/56433539/43585dc2-adb3-45c6-8988-efc5c9019904)


