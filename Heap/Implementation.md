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
    this.heap[this.heap.length] = key;
    this.heapifyUp();
  }

  heapifyUp() {
    let currentIndex = this.heap.length - 1;

    while (this.heap[currentIndex] < this.heap[this.getParentIndex(currentIndex)]) {
      this.swapIndex(currentIndex, this.getParentIndex(currentIndex));
      currentIndex = this.getParentIndex(currentIndex);
    }
  }

  pop() {
    let minValue = this.heap[0];
    this.heap[0] = this.heap[this.heap.length - 1];
    this.heap.length--;
    this.heapifyDown();
    return minValue;
  }

  heapifyDown() {
    let currentIndex = 0;

    while (this.heap[this.getLeftChildIndex(currentIndex)] !== undefined) {
      let smallestChildIndex = this.getLeftChildIndex(currentIndex);
      let rightChildIndex = this.getRightChildIndex(currentIndex);
      let leftChildIndex = this.getLeftChildIndex(currentIndex);

      if (this.heap[rightChildIndex] && this.heap[rightChildIndex] < this.heap[leftChildIndex]) {
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

  peek() {
    return this.heap[0];
  }

  size() {
    return this.heap.length;
  }

  isEmpty() {
    return this.heap.length === 0;
  }

  buildHeap(array) {
    this.heap = array;
    for (let i = Math.floor(this.heap.length / 2); i >= 0; i--) {
      this.heapifyDown(i);
    }
  }

  updateKey(index, newValue) {
    if (index < 0 || index >= this.heap.length) {
      return;
    }
    this.heap[index] = newValue;
    this.heapifyUp(index);
    this.heapifyDown(index);
  }

  removeKey(index) {
    if (index < 0 || index >= this.heap.length) {
      return;
    }
    this.swapIndex(index, this.heap.length - 1);
    this.heap.pop();
    this.heapifyUp(index);
    this.heapifyDown(index);
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
    this.heap[this.heap.length] = key;
    this.heapifyUp();
  }

  heapifyUp() {
    let currentIndex = this.heap.length - 1;

    while (this.heap[currentIndex] > this.heap[this.getParentIndex(currentIndex)]) {
      this.swapIndex(currentIndex, this.getParentIndex(currentIndex));
      currentIndex = this.getParentIndex(currentIndex);
    }
  }

  pop() {
    let maxValue = this.heap[0];
    this.heap[0] = this.heap[this.heap.length - 1];
    this.heap.length--;
    this.heapifyDown();
    return maxValue;
  }

  heapifyDown() {
    let currentIndex = 0;

    while (this.heap[this.getLeftChildIndex(currentIndex)] !== undefined) {
      let biggestChildIndex = this.getLeftChildIndex(currentIndex);
      let rightChildIndex = this.getRightChildIndex(currentIndex);
      let leftChildIndex = this.getLeftChildIndex(currentIndex);

      if (this.heap[rightChildIndex] && this.heap[rightChildIndex] > this.heap[leftChildIndex]) {
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

  peek() {
    return this.heap[0];
  }

  size() {
    return this.heap.length;
  }

  isEmpty() {
    return this.heap.length === 0;
  }

  buildHeap(array) {
    this.heap = array;
    for (let i = Math.floor(this.heap.length / 2); i >= 0; i--) {
      this.heapifyDown(i);
    }
  }

  updateKey(index, newValue) {
    if (index < 0 || index >= this.heap.length) {
      return;
    }
    this.heap[index] = newValue;
    this.heapifyUp(index);
    this.heapifyDown(index);
  }

  removeKey(index) {
    if (index < 0 || index >= this.heap.length) {
      return;
    }
    this.swapIndex(index, this.heap.length - 1);
    this.heap.pop();
    this.heapifyUp(index);
    this.heapifyDown(index);
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

