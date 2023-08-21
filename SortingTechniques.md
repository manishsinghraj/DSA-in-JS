### 1. Selection sort
```js
const selectionSort = (arr, n) => {

    for (let i = 0; i <= n - 2; i++) {
        let min = i; //setting current position(first element of unsorted array)
        for (let j = i; j <= n - 1; j++) {
            if (arr[j] < arr[min]) {
                min = j;
            }
        }
        if (min !== i) {
            let temp = arr[min];
            arr[min] = arr[i];
            arr[i] = temp;
        }
    }
    return arr;
}

var arr = [13, 46, 24, 52, 20, 9, 1];
console.log(selectionSort(arr, arr.length));
```

### 2. BubbleSort

```js
const bubbleSort1 = (arr, n) => {
    for (let i = n - 1; i >= 0; i--) {
        for (let j = 0; j <= i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                let temp = arr[j + 1];
                arr[j + 1] = arr[j];
                arr[j] = temp;
            }
        }
    }

    return arr;
}

var arr = [13, 46, 24, 52, 20, 9];
console.log(bubbleSort1(arr, arr.length));


const bubbleSort2 = (arr, n) => {
    for (let i = 0; i <= n - 1; i++) {
        let isSwapped = false;
        for (let j = 0; j <= n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                let temp = arr[j + 1];
                arr[j + 1] = arr[j];
                arr[j] = temp;
                isSwapped = true;
            }
        }

        if (isSwapped == false) {
            break;
        }
    }

    return arr;
}

var arr = [1, 2, 3, 4, 5];
console.log(bubbleSort2(arr, arr.length));
```

### 3. InsertionSort

```js
const insertionSort = (arr, n) => {
    for (let i = 0; i <= n - 1; i++) {
        let j = i;
        while (j > 0 && arr[j - 1] > arr[j]) {
            var temp = arr[j - 1];
            arr[j - 1] = arr[j];
            arr[j] = temp;
            j--;
        }
    }

    return arr;
}

var arr = [13, 46, 24, 52, 20, 9];
console.log(insertionSort(arr, arr.length));
```


### 4. Merge Sort
```js
const mergeSort = (arr, low, high) => {
    // Base condition
    if (low >= high) return;

    let mid = Math.floor((low + high) / 2);
    // Divide
    mergeSort(arr, low, mid);
    mergeSort(arr, mid + 1, high);
    // Merge
    merge(arr, low, mid, high);
    return arr

}

const merge = (arr, low, mid, high) => {
    let temp = [];
    // compare by pointers left and right arays
    // 2 pointers
    let left = low;
    let right = mid + 1;
    while (left <= mid && right <= high) {
        if (arr[left] <= arr[right]) {
            temp.push(arr[left]);
            left++;
        } else {
            temp.push(arr[right]);
            right++;
        }
    }

    while (left <= mid) {
        temp.push(arr[left]);
        left++;
    }

    while (right <= high) {
        temp.push(arr[right]);
        right++;
    }

    for (let i = low; i <= high; i++) {
        arr[i] = temp[i - low];
    }

    return arr;
}

var arr = [4, 3, 5, 1, 3, 8, 9, 12, 6];
var low = 0;
var high = arr.length - 1;
console.log(mergeSort(arr, low, high));
```


### 5. QuickSort
```js
const quickSort = (arr, low, high) => {

    if (low < high) {
        let pIndex = partition(arr, low, high);
        quickSort(arr, low, pIndex - 1);
        quickSort(arr, pIndex + 1, high);
    }
    return arr;
}

const partition = (arr, low, high) => {
    let pivot = low;
    i = low;
    j = high;

    while (i < j) {
        while (arr[i] <= arr[pivot] && i <= high - 1) {
            i++;
        }

        while (arr[j] > arr[pivot] && j >= low + 1) {
            j--;
        }

        if (i < j) {
            swap
            [arr[i], arr[j]] = [arr[j], arr[i]];
        }
    }
    //swap
    [arr[pivot], arr[j]] = [arr[j], arr[pivot]];
    return j;
}

var arr = [2, 5, 8, 1, 3, 6];
var low = 0;
console.log(quickSort(arr, low, arr.length - 1));
```