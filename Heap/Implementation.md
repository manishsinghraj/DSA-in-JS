# Min Heap

```javascript
class MinHeap {
  constructor() {
    this.heap = [];
  }

  getParentIndex(index) {
    return Math.floor((index - 1) / 2);
  }

  getLeftChildIndex(index) {
    return 2 * index + 1;
  }

  getRightChildIndex(index) {
    return 2 * index + 2;
  }

  swapIndex(index1, index2) {
    [this.heap[index1], this.heap[index2]] = [this.heap[index2], this.heap[index1]];
  }

  push(key) {
    this.heap.push(key);
    this.heapifyUp();
  }

  heapifyUp() {
    let currentIndex = this.heap.length - 1;

    while (currentIndex > 0 && this.heap[currentIndex] < this.heap[this.getParentIndex(currentIndex)]) {
      this.swapIndex(currentIndex, this.getParentIndex(currentIndex));
      currentIndex = this.getParentIndex(currentIndex);
    }
  }

  pop() {
    if (this.heap.length === 0) {
      return null;
    }

    const minValue = this.heap[0];
    this.heap[0] = this.heap[this.heap.length - 1];
    this.heap.length--;
    this.heapifyDown(0);
    return minValue;
  }

  heapifyDown(index) {
    let currentIndex = index;

    while (this.getLeftChildIndex(currentIndex) < this.heap.length) {
      let smallestChildIndex = this.getLeftChildIndex(currentIndex);
      const rightChildIndex = this.getRightChildIndex(currentIndex);
      const leftChildIndex = this.getLeftChildIndex(currentIndex);

      if (rightChildIndex < this.heap.length && this.heap[rightChildIndex] < this.heap[leftChildIndex]) {
        smallestChildIndex = rightChildIndex;
      }

      if (this.heap[currentIndex] > this.heap[smallestChildIndex]) {
        this.swapIndex(currentIndex, smallestChildIndex);
        currentIndex = smallestChildIndex;
      } else {
        return;
      }
    }
  }
}

// Example usage:
const minHeap = new MinHeap();
minHeap.push(4);
minHeap.push(8);
minHeap.push(2);
minHeap.push(5);

console.log(minHeap.heap); // Output: [2, 4, 8, 5]

console.log(minHeap.pop()); // Output: 2
console.log(minHeap.heap); // Output: [4, 5, 8]
```


<hr>


# Max Heap


```javascript
class MaxHeap {
  constructor() {
    this.heap = [];
  }

  getParentIndex(index) {
    return Math.floor((index - 1) / 2);
  }

  getLeftChildIndex(index) {
    return 2 * index + 1;
  }

  getRightChildIndex(index) {
    return 2 * index + 2;
  }

  swapIndex(index1, index2) {
    [this.heap[index1], this.heap[index2]] = [this.heap[index2], this.heap[index1]];
  }

  push(key) {
    this.heap.push(key);
    this.heapifyUp();
  }

  heapifyUp() {
    let currentIndex = this.heap.length - 1;

    while (currentIndex > 0 && this.heap[currentIndex] > this.heap[this.getParentIndex(currentIndex)]) {
      this.swapIndex(currentIndex, this.getParentIndex(currentIndex));
      currentIndex = this.getParentIndex(currentIndex);
    }
  }

  pop() {
    if (this.heap.length === 0) {
      return null;
    }

    const maxValue = this.heap[0];
    this.heap[0] = this.heap[this.heap.length - 1];
    this.heap.length--;
    this.heapifyDown(0);
    return maxValue;
  }

  heapifyDown(index) {
    let currentIndex = index;

    while (this.getLeftChildIndex(currentIndex) < this.heap.length) {
      let biggestChildIndex = this.getLeftChildIndex(currentIndex);
      const rightChildIndex = this.getRightChildIndex(currentIndex);
      const leftChildIndex = this.getLeftChildIndex(currentIndex);

      if (rightChildIndex < this.heap.length && this.heap[rightChildIndex] > this.heap[leftChildIndex]) {
        biggestChildIndex = rightChildIndex;
      }

      if (this.heap[currentIndex] < this.heap[biggestChildIndex]) {
        this.swapIndex(currentIndex, biggestChildIndex);
        currentIndex = biggestChildIndex;
      } else {
        return;
      }
    }
  }
}

// Example usage:
const maxHeap = new MaxHeap();
maxHeap.push(4);
maxHeap.push(8);
maxHeap.push(2);
maxHeap.push(5);

console.log(maxHeap.heap); // Output: [8, 5, 2, 4]

console.log(maxHeap.pop()); // Output: 8
console.log(maxHeap.heap); // Output: [5, 4, 2]
```

