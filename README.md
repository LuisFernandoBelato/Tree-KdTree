## 🌐 Language | Idioma

[🇺🇸 English (Default)](#en) | [🇧🇷 Português](#pt)

<div id="en"></div>

---

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

<div id="pt"></div>

---

# Implementação de Árvore K-d Tree em C \ ***4º Termo - Estruturas de Dados II***

Este projeto implementa uma K-d Tree para organizar pontos em um espaço de K dimensões e realizar buscas por proximidade (busca por raio). O desenvolvimento segue as especificações do trabalho de Estruturas de Dados II.

## Visão Geral do Projeto

O objetivo principal é construir uma K-d Tree a partir de um conjunto de pontos e, em seguida, utilizar essa árvore para encontrar todos os pontos que estão dentro de um raio específico de uma dada coordenada.

## Funcionalidades

*   **Construção da K-d Tree:**
    *   Suporta K dimensões (definido pela macro `K`).
    *   Os pontos podem ser gerados aleatoriamente ou carregados a partir de um conjunto pré-definido (função `EncheVetorChico` para teste, `EncheVetorRandom` para geração aleatória).
    *   A árvore é construída recursivamente, alternando o eixo de divisão (dimensão) em cada nível.
    *   Em cada etapa, o conjunto de pontos é ordenado pela dimensão atual e o ponto mediano é escolhido para dividir o espaço.
*   **Busca por Raio**
    *   Dada uma coordenada de referência e um raio, a função de busca percorre a K-d Tree para encontrar todos os pontos que estão dentro da distância euclidiana especificada pelo raio.
*   **Exibição da Árvore:**
    *   Uma função para exibir a estrutura da K-d Tree no console em um formato hierárquico (árvore deitada).
*   **Geração de Dados:**
    *   Pontos e a coordenada de busca/raio podem ser gerados aleatoriamente para facilitar os testes.

## Como Funciona

### 1. Estrutura de Dados

*   **`struct KdTree`**: Representa um nó na K-d Tree. Cada nó armazena:
    *   `ponto[K]`: Um array de inteiros contendo as coordenadas do ponto no espaço K-dimensional.
    *   `esq`: Ponteiro para o filho esquerdo (pontos com valor menor na dimensão de corte atual).
    *   `dir`: Ponteiro para o filho direito (pontos com valor maior na dimensão de corte atual).

### 2. Construção da Árvore (`CriaKdTree`)

1.  **Inicialização:**
    *   Um conjunto de pontos é gerado (aleatoriamente ou fixo).
2.  **Processo Recursivo:**
    *   A função `CriaKdTree` recebe o conjunto de pontos atual, o nível atual da árvore (para determinar a dimensão de corte) e os índices de início e fim do subconjunto de pontos a ser processado.
    *   **Seleção da Dimensão de Corte (Discriminante):** A dimensão é determinada pelo `nivel % K` (alternando entre 0, 1, ..., K-1).
    *   **Ordenação:** O subconjunto de pontos é ordenado com base na coordenada da dimensão de corte atual.
    *   **Seleção do Ponto Mediano:** O ponto na posição mediana do subconjunto ordenado é escolhido para ser o nó atual da árvore.
    *   **Criação do Nó:** Um novo nó é criado com o ponto mediano.
    *   **Recursão:** A função é chamada recursivamente para:
        *   O subconjunto à esquerda do mediano (para o filho esquerdo), incrementando o nível.
        *   O subconjunto à direita do mediano (para o filho direito), incrementando o nível.
    *   O processo continua até que os subconjuntos não possam mais ser divididos (início > fim).

### 3. Busca por Raio (`BuscaPontos`)

1.  **Entrada:** Um nó da árvore (inicialmente a raiz), a coordenada de busca e o raio.
2.  **Cálculo da Distância Euclidiana:** Para o ponto no nó atual, a distância euclidiana até a coordenada de busca é calculada:
    `sqrt(sum((ponto_arvore[i] - ponto_busca[i])^2))`
3.  **Verificação:**
    *   Se a distância calculada for menor ou igual ao raio, o ponto do nó atual é considerado "próximo" e é exibido.
4.  **Poda e Recursão (Simplificada na Implementação Atual):**
    *   A implementação fornecida explora o filho direito se o ponto atual estiver dentro do raio e o filho direito existir.
    *   Explora o filho esquerdo independentemente (se existir).
    *   *Nota: Uma busca por raio mais otimizada em K-d Trees geralmente envolve verificar se a hiperesfera de busca intercepta os hiperplanos de divisão para decidir se é necessário explorar as subárvores. A implementação atual é uma busca mais direta.*

### 4. Exibição (`ExibeArvoreKdTree`)

*   Utiliza um percurso em ordem (modificado) para imprimir os nós. A recursão para a direita é feita primeiro, depois o nó atual é impresso com indentação baseada na profundidade, e então a recursão para a esquerda. Isso resulta em uma visualização da árvore "deitada".

---

## Estrutura do Código

*   **Definições Globais:** Constantes para `K` (dimensões), `TAM` (número de pontos a gerar), `MAX` (valor máximo para coordenadas).
*   **Estruturas:** Definição de `struct KdTree`.
*   **Funções Auxiliares:**
    *   `CriaNo`: Aloca e inicializa um novo nó da K-d Tree.
    *   `EncheVetorChico`: Preenche um vetor com pontos pré-definidos para teste.
    *   `Muda_Coordenadas`: Troca as coordenadas de dois pontos.
    *   `ExibeCoordenadasMatriz`: Mostra todos os pontos de uma matriz.
    *   `Ordena`: Ordena um subconjunto de pontos com base em uma dimensão específica (usado na construção da árvore).
    *   `MostraCoordenada`: Exibe um único ponto.
    *   `MostraNaTree`: Exibe o ponto de um nó da árvore.
    *   `GeraCoordenada`: Gera uma coordenada aleatória.
*   **Funções Principais:**
    *   `EncheVetorRandom`: Preenche a matriz de pontos com coordenadas aleatórias.
    *   `CriaKdTree`: Função recursiva para construir a K-d Tree.
    *   `CalculoDistanciaEuclidiana`: Calcula a distância entre um ponto da árvore e a coordenada de busca.
    *   `BuscaPontos`: Realiza a busca por raio.
    *   `ExibeArvoreKdTree`: Exibe a árvore formatada.
*   **`main()`:**
    *   Inicializa o gerador de números aleatórios.
    *   Declara a raiz da K-d Tree e outras variáveis necessárias.
    *   Preenche o vetor de pontos (usando `EncheVetorRandom` ou `EncheVetorChico`).
    *   Exibe os pontos gerados e um exemplo de ordenação.
    *   Chama `CriaKdTree` para construir a árvore.
    *   Exibe a K-d Tree formada.
    *   Gera uma coordenada de busca e um raio aleatórios.
    *   Chama `BuscaPontos` para encontrar e exibir os pontos próximos.
