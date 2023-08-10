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

## Methodology

### Chromosome Representation
Each Chromosome is an 81 characters long string encoding the information about every 81 cells of the Sudoku. Each gene represents the color assigned to each cell. The possible value of each gene lies between 1 to 9. The ith gene of Chromosome is represented by C[i].

### Fitness
**Bad Edge** - A bad edge is defined as an edge connecting two vertices that have the same color.

The fitness of each individual is the number of bad edges in the colored graph that the chromosome represents.

```math
fitness(C,Adj) = \sum\limits_{i=0}^{80} \sum\limits_{j=0}^{80} [C[i] = C[j] \land Adj[i][j] = 1]
```

### Parent Selection
Parent selection is a critical component of genetic algorithms that determines how individuals in a population are selected for mating and reproduction to create new offspring. The goal of parent selection is to identify the fittest individuals that have a higher probability of producing better offspring.

#### Parent Selection 1
Parent selection 1 is tournament selection. In this method, a small subset of individuals is randomly selected from the population, and the fittest individual is chosen as a parent. This process is repeated until the desired number of parents is selected.

#### Parent Selection 2
Parent selection 2 selects the best and the second-best individual of the population.

### Crossover
One-point crossover is used to recombine two parent chromosomes to generate new offspring. It works by selecting a random crossover point along the length of both parents and then swapping the genetic material beyond that point. This creates two new offspring, each with genetic material from both parents.

### Mutation
The mutation is a genetic operator used in evolutionary algorithms, including genetic algorithms, to introduce genetic diversity in the population of solutions. It is used to prevent premature convergence and to explore the search space. Two Mutation operators have been used in this paper:

#### Mutation 1
The mutation 1 operator takes a chromosome as input and checks if any vertex in the graph has the same color as its adjacent vertices. If this condition is true, it creates a list of all adjacent colors and a list of all possible colors. It then removes the adjacent colors from the list of all possible colors to create a list of valid colors. Next, it randomly selects a valid color from the list and assigns it to the vertex that failed the color test. The mutation of a node is done with probability 0.2. Finally, it returns the mutated chromosome.

#### Mutation 2
For each vertex in the chromosome, mutation 2 checks if the vertex has the same color as any of its adjacent vertices. If it does, a new color is randomly chosen from the full set of available colors and assigned to the vertex. The mutation probability of this operator is 0.6. Finally, the mutated chromosome is returned.

### Working Process
- The population is initialized with individuals of 81 length with each empty position having a random color between 1 to 9.
- Selection, Crossover, and Mutation are performed for each individual of the population in each generation.
- The algorithm randomly switches between the 2 defined mutation and parent selection strategies.
- The fitness is calculated after each generation of the population and the best individual solution is displayed.
- The algorithm terminates when it had run for the specified number of generations or when it finds an individual with 0 fitness value.

## Results

The result, as in Fig 4, is obtained for the input as shown in Fig 3. This problem was solved in 3008 generations and the population size was 500.\\
The Fig 6 shows the best-fitness vs number of generation graph for the given problem.

![input](https://github.com/SamarpreetSingh/Sudoku-Solver-with-Graph-Coloring-using-Genetic-Algorithm/assets/56433539/fdcfa5fc-e410-43ef-937e-2068e6516112 "Input")

![Output](https://github.com/SamarpreetSingh/Sudoku-Solver-with-Graph-Coloring-using-Genetic-Algorithm/assets/56433539/ae138f17-082f-4f16-809f-0e8204d4f137)
![best-fitness vs generations](https://github.com/SamarpreetSingh/Sudoku-Solver-with-Graph-Coloring-using-Genetic-Algorithm/assets/56433539/0fc2c534-0278-44c1-a3c8-7fd079b24990)

## Conclusion

In conclusion, this research paper presents an approach for solving Sudoku puzzles using a combination of graph theory and genetic algorithms. The proposed algorithm represents Sudoku puzzles as graphs and employs graph coloring to solve them. The genetic algorithm is used to optimize the graph coloring solution and utilizes multiple parent selection and mutation methods on a randomized basis to reach the global optimum quickly. The results demonstrate that the proposed algorithm successfully solved a sample Sudoku puzzle. This approach has the potential to be extended to other optimization problems that can be represented as graphs. Overall, this research contributes to the field of optimization and puzzle-solving by offering a new technique that combines graph theory and genetic algorithms.

## References

1. Hindi, Musa & Yampolskiy, Roman. "Genetic Algorithm Applied to the Graph Coloring Problem." Midwest Artificial Intelligence and Cognitive.
2. Díaz, Isabel Méndez, and Zabala, Paula. "A Generalization of the Graph Coloring Problem." Departamento de Computacion, Universidad de Buenos Aires.
3. Chatterjee, Sankhadeep & Paladhi, Saubhik & Chakraborty, Raktim. "A Comparative Study On The Performance Characteristics Of Sudoku Solving Algorithms." IOSR Journal of Computer Engineering.
4. Deb, K. "An introduction to genetic algorithms." Sadhana, 24, 293-315.


