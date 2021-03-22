# WEEK 4

## 4 Leftist Heaps and Skew Heaps

### 4.1 Leftist Heaps

- **Target**: Speed up merging in $O(N)$

- Heap: Structure Property + Order Property
- Leftist Heap
  - Order Property – the same
  - Structure Property – binary tree, but **unbalanced**

#### [Definition] The *null path length*, Npl(X), of any node X is the length of the shortest path from X to a node without two children.  Define Npl(NULL) = –1.

> Note: Npl(X) = min{ Npl(C) + 1 for all C as children of X }

#### [Definition] The *leftist heap property* is that for every node X in the heap, the null path length of the left child is *at least as large as* that of the right child.

- The tree is biased to get deep toward the left.

#### [Theorem] A leftist tree with $r$ nodes on the right path must have at least $2^r – 1$ nodes.

> Note: The leftist tree of $N$ nodes has a right path containing at most $\lfloor\log_2(N+1)\rfloor$ nodes.

- We can perform all the work on the right pat, which is guaranteed to be short
- Trouble makers: Insert and Merge

> Note: Insertion is merely a special case of merging.

#### Declaration

```c
struct TreeNode 
{ 
	ElementType	Element;
	PriorityQueue Left;
	PriorityQueue ight;
	int Npl;
};
```

#### Merge (recursive version)

<img src="picture/image-20210322104338208.png" alt="image-20210322104338208" style="zoom:80%;" />

- Step 1: Merge( H1->Right, H2 )

  <img src="picture/image-20210322104407180.png" alt="image-20210322104407180" style="zoom:80%;" />

- Step 2: Attach( H2, H1->Right )

  <img src="picture/image-20210322104510239.png" alt="image-20210322104510239" style="zoom:80%;" />

- Step 3: Swap(H1->Right, H1->Left ) if necessary