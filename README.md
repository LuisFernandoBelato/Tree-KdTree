# K-d Tree Implementation in C \ ***4th Term - Data Structures II***

This project implements a K-d Tree to organize points in a K-dimensional space and perform proximity searches (radius search). The development follows the specifications of the Data Structures II assignment.

## Project Overview

The main objective is to build a K-d Tree from a set of points and then use this tree to find all points that are within a specific radius of a given coordinate.

## Features

*   **K-d Tree Construction:**
    *   Supports K dimensions (defined by the macro `K`).
    *   Points can be generated randomly or loaded from a predefined set (`EncheVetorChico` function for testing, `EncheVetorRandom` for random generation).
    *   The tree is built recursively, alternating the splitting axis (dimension) at each level.
    *   At each step, the set of points is sorted by the current dimension, and the median point is chosen to split the space.
*   **Radius Search:**
    *   Given a reference coordinate and a radius, the search function traverses the K-d Tree to find all points within the Euclidean distance specified by the radius.
*   **Tree Display:**
    *   A function to display the K-d Tree structure in the console in a hierarchical format (horizontal tree).
*   **Data Generation:**
    *   Points and the search coordinate/radius can be generated randomly to facilitate testing.

## How It Works

### 1. Data Structure

*   **`struct KdTree`**: Represents a node in the K-d Tree. Each node stores:
    *   `ponto[K]`: An integer array containing the point's coordinates in K-dimensional space.
    *   `esq`: Pointer to the left child (points with a smaller value in the current splitting dimension).
    *   `dir`: Pointer to the right child (points with a larger value in the current splitting dimension).

### 2. Tree Construction (`CriaKdTree`)

1.  **Initialization:**
    *   A set of points is generated (randomly or fixed).
2.  **Recursive Process:**
    *   The `CriaKdTree` function receives the current set of points, the current tree level (to determine the splitting dimension), and the start and end indices of the subset of points to be processed.
    *   **Splitting Dimension Selection (Discriminator):** The dimension is determined by `level % K` (alternating between 0, 1, ..., K-1).
    *   **Sorting:** The subset of points is sorted based on the coordinate of the current splitting dimension.
    *   **Median Point Selection:** The point at the median position of the sorted subset is chosen to be the current tree node.
    *   **Node Creation:** A new node is created with the median point.
    *   **Recursion:** The function is called recursively for:
        *   The subset to the left of the median (for the left child), incrementing the level.
        *   The subset to the right of the median (for the right child), incrementing the level.
    *   The process continues until the subsets can no longer be divided (start > end).

### 3. Radius Search (`BuscaPontos`)

1.  **Input:** A tree node (initially the root), the search coordinate, and the radius.
2.  **Euclidean Distance Calculation:** For the point in the current node, the Euclidean distance to the search coordinate is calculated:
    `sqrt(sum((ponto_arvore[i] - ponto_busca[i])^2))`
3.  **Verification:**
    *   If the calculated distance is less than or equal to the radius, the point in the current node is considered "close" and is displayed.
4.  **Pruning and Recursion (Simplified in Current Implementation):**
    *   The provided implementation explores the right child if the current point is within the radius and the right child exists.
    *   It explores the left child independently (if it exists).
    *   *Note: A more optimized radius search in K-d Trees usually involves checking if the search hypersphere intersects the splitting hyperplanes to decide whether to explore subtrees. The current implementation is a more direct search.*

### 4. Display (`ExibeArvoreKdTree`)

*   Uses a (modified) in-order traversal to print the nodes. The recursion to the right is done first, then the current node is printed with indentation based on depth, and then the recursion to the left. This results in a "horizontal" tree visualization.

---

## Code Structure

*   **Global Definitions:** Constants for `K` (dimensions), `TAM` (number of points to generate), `MAX` (maximum value for coordinates).
*   **Structures:** Definition of `struct KdTree`.
*   **Auxiliary Functions:**
    *   `CriaNo`: Allocates and initializes a new K-d Tree node.
    *   `EncheVetorChico`: Fills a vector with predefined points for testing.
    *   `Muda_Coordenadas`: Swaps the coordinates of two points.
    *   `ExibeCoordenadasMatriz`: Shows all points in a matrix.
    *   `Ordena`: Sorts a subset of points based on a specific dimension (used in tree construction).
    *   `MostraCoordenada`: Displays a single point.
    *   `MostraNaTree`: Displays the point of a tree node.
    *   `GeraCoordenada`: Generates a random coordinate.
*   **Main Functions:**
    *   `EncheVetorRandom`: Fills the point matrix with random coordinates.
    *   `CriaKdTree`: Recursive function to build the K-d Tree.
    *   `CalculoDistanciaEuclidiana`: Calculates the distance between a tree point and the search coordinate.
    *   `BuscaPontos`: Performs the radius search.
    *   `ExibeArvoreKdTree`: Displays the formatted tree.
*   **`main()`:**
    *   Initializes the random number generator.
    *   Declares the K-d Tree root and other necessary variables.
    *   Fills the point vector (using `EncheVetorRandom` or `EncheVetorChico`).
    *   Displays the generated points and a sorting example.
    *   Calls `CriaKdTree` to build the tree.
    *   Displays the formed K-d Tree.
    *   Generates a random search coordinate and radius.
    *   Calls `BuscaPontos` to find and display nearby points.
