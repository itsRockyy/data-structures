# Heaps

> ## A Heap is a special Tree-based data structure in which the tree is a complete binary tree.

Generally, Heaps can be of two types:

- `Max-Heap` : In a Max-Heap the key present at the root node must be greatest among the keys present at all of it’s children. The same property must be recursively true for all sub-trees in that Binary Tree.
- `Min-Heap` : In a Min-Heap the key present at the root node must be minimum among the keys present at all of it’s children. The same property must be recursively true for all sub-trees in that Binary Tree.

## Binary Heaps

It’s a complete tree (All levels are completely filled except possibly the last level and the last level has all keys as left as possible). This property of Binary Heap makes them suitable to be stored in an array.

## Fibonacci Heaps

Fibonacci heap is a modified form of a binomial heap with more efficient heap operations than that supported by the binomial and binary heaps.

Unlike binary heap, a node can have more than two children.

The fibonacci heap is called a fibonacci heap because the trees are constructed in a way such that a tree of order n has at least Fn+2 nodes in it, where Fn+2 is the (n + 2)nd Fibonacci number.

## Operations

- `Heapify` : Heapify is the process of creating a heap data structure from a binary tree. It is used to create a Min-Heap or a Max-Heap
- `insert` : Insert an Element into Heap
- `remove` : Remove an Element from Heap
- `peek` : Peek operation returns the maximum element from Max Heap or minimum element from Min Heap without deleting the node
- `extract` : Extract-Max returns the node with maximum value after removing it from a Max Heap whereas Extract-Min returns the node with minimum after removing it from Min Heap

## Heap Applications

- Heap is used while implementing a priority queue.
- Dijkstra’s Algorithm
- Heap Sort

## Implementation (Min Binary Heap)

```js
class MinBinaryHeap {
  constructor() {
    this.values = [];
  }

  bubbleUp() {
    let index = this.values.length - 1;
    const elem = this.values[index];

    while (index > 0) {
      const parentIndex = Math.floor((index - 1) / 2);
      const parent = this.values[parentIndex];

      if (elem > parent) break;
      this.values[parentIndex] = elem;
      this.values[index] = parent;
      index = parentIndex;
    }
  }

  sinkDown() {
    let index = 0;
    const elem = this.values[0];
    const length = this.values.length;

    while (index !== null) {
      let leftIndex = 2 * index + 1;
      let rightIndex = 2 * index + 2;
      let swapIndex = null;

      if (leftIndex < length && elem > this.values[leftIndex]) {
        swapIndex = leftIndex;
      }

      if (rightIndex < length && elem > this.values[rightIndex]) {
        swapIndex =
          this.values[rightIndex] > this.values[leftIndex]
            ? rightIndex
            : leftIndex;
      }

      if (swapIndex == null) break;

      this.values[index] = this.values[swapIndex];
      this.values[swapIndex] = elem;

      index = swapIndex;
    }
  }

  insert(val) {
    this.values.push(val);
    this.bubbleUp();
  }

  extractMin() {
    const min = this.values[0];
    const end = this.values.pop();

    if (this.values.length) {
      this.values[0] = end;
      this.sinkDown();
    }

    return min;
  }
}

const heap = new MinBinaryHeap();
heap.insert(41);
heap.insert(39);
heap.insert(33);
heap.insert(18);
heap.insert(27);
heap.insert(12);
heap.insert(55);

console.log(heap.values);
console.log(heap.extractMin());
console.log(heap.values);
console.log(heap.extractMin());
console.log(heap.values);
```

## Implementation (Max Binary Heap)

```js
class MaxBinaryHeap {
  constructor() {
    this.values = [];
  }

  bubbleUp() {
    let index = this.values.length - 1;
    const elem = this.values[index];

    while (index > 0) {
      const parentIndex = Math.floor((index - 1) / 2);
      const parent = this.values[parentIndex];

      if (elem < parent) break;
      this.values[parentIndex] = elem;
      this.values[index] = parent;
      index = parentIndex;
    }
  }

  sinkDown() {
    let index = 0;
    const elem = this.values[0];
    const length = this.values.length;

    while (index !== null) {
      const leftIndex = 2 * index + 1;
      const rightIndex = 2 * index + 2;
      let swapIndex = null;

      if (leftIndex < length && elem < this.values[leftIndex]) {
        swapIndex = leftIndex;
      }

      if (rightIndex < length && elem < this.values[rightIndex]) {
        swapIndex =
          this.values[rightIndex] > this.values[leftIndex]
            ? rightIndex
            : leftIndex;
      }

      if (swapIndex == null) break;

      this.values[index] = this.values[swapIndex];
      this.values[swapIndex] = elem;

      index = swapIndex;
    }
  }

  insert(val) {
    this.values.push(val);
    this.bubbleUp();
  }

  extractMax() {
    const max = this.values[0];
    const end = this.values.pop();

    if (this.values.length) {
      this.values[0] = end;
      this.sinkDown();
    }

    return max;
  }
}

const heap = new MaxBinaryHeap();
heap.insert(41);
heap.insert(39);
heap.insert(33);
heap.insert(18);
heap.insert(27);
heap.insert(12);
heap.insert(55);

console.log(heap.values);
console.log(heap.extractMax());
console.log(heap.values);
console.log(heap.extractMax());
console.log(heap.extractMax());
console.log(heap.values);
```
