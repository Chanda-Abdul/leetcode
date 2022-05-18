# ❗ Sort Algorithms
[https://www.freecodecamp.org/learn/coding-interview-prep/#algorithms](https://www.freecodecamp.org/learn/coding-interview-prep/#algorithms)

Given an array of unsorted items, we want to be able to return a sorted array. We will see several different methods to do this and learn some tradeoffs between these different approaches. While most modern languages have built-in sorting methods for operations like this, it is still important to understand some of the common basic approaches and learn how they can be implemented.


## Bubble Sort
Here we will see <b>bubble sort</b>. The <b>bubble sort</b> method starts at the beginning of an unsorted array and <b>'bubbles up'</b> unsorted values towards the end, iterating through the array until it is completely sorted. It does this by comparing adjacent items and swapping them if they are out of order. The method continues looping through the array until no swaps occur at which point the array is sorted.

This method requires multiple iterations through the array and for average and worst cases has <b>quadratic time complexity</b>. While simple, it is usually impractical in most situations.
````js
function bubbleSort(array) {
  for (let i = 0; i < array.length; i++) {
    // -i because the largest element will be bubbled at the end so we don't have to compare.
    for (let j = 0; j < array.length - 1 - i; j++) {
      if (array[j] > array[j + 1])
        [array[j], array[j + 1]] = [array[j + 1], array[j]]; 
    }
  }
  return array;
}

 bubbleSort([1,4,2,8,345,123,43,32,5643,63,123,43,2,55,1,234,92])
````
## Selection Sort
<b>Selection sort</b> works by selecting the minimum value in a list and swapping it with the first value in the list. It then starts at the second position, selects the smallest value in the remaining list, and swaps it with the second element. It continues iterating through the list and swapping elements until it reaches the end of the list. Now the list is sorted. <b>Selection sort</b> has quadratic time complexity in all cases.
````js
function selectionSort(array) {
  for (let i = 0; i < array.length - 1; i++) {
    let min = i;
    for (let j = i + 1; j < array.length; j++) {
      if (array[min] > array[j]) min = j;
    }
    //swap
    [array[i], array[min]] = [array[min], array[i]]
  }
  return array;
}

 selectionSort([1,4,2,8,345,123,43,32,5643,63,123,43,2,55,1,234,92])
````
## Insertion Sort
This method works by building up a sorted array at the beginning of the list. It begins the sorted array with the first element. Then it inspects the next element and swaps it backwards into the sorted array until it is in sorted position. It continues iterating through the list and swapping new items backwards into the sorted portion until it reaches the end. This algorithm has quadratic time complexity in the average and worst cases.
````js
function insertionSort(array) {
  for (let i = 0; i < array.length-1; i++) {
    for (let j = i+1; j < array.length; j++)  {
      if(array[i] > array[j]){
        [array[i], array[j]] = [array[j],array[i]]
      }
    }
  }
  return array;
}

insertionSort([1,4,2,8,345,123,43,32,5643,63,123,43,2,55,1,234,92]) 
//should return an array that is unchanged except for order.
insertionSort([5, 4, 33, 2, 8]) 
//[2, 4, 5, 8, 33]
````
## 🔍 Quick Sort
##### https://youtu.be/P6XGSKO2RzI
<b>Quick sort</b> is an efficient, recursive divide-and-conquer approach to sorting an array. In this method, a `pivot` value is chosen in the original array. The array is then partitioned into two subarrays of values less than and greater than the `pivot` value. We then combine the result of recursively calling the <b>quick sort</b> algorithm on both sub-arrays. This continues until the base case of an empty or single-item array is reached, which we return. The unwinding of the recursive calls return us the sorted array.

<b>Quick sort</b> is a very efficient sorting method, providing `O(nlog(n))` performance on average. It is also relatively easy to implement. These attributes make it a popular and useful sorting method.
````js
function quickSort(array) {
  //base case
  if (array.length === 1) return array;
  
  //pivot on end value
  const pivotPoint = array[array.length-1];
  const firstHalf = [];
  const secondHalf = [];
  
  for(let i = 0; i < array.length-1; i++) {
    if(array[i] < pivotPoint){
      firstHalf.push(array[i])
    }else {
      secondHalf.push(array[i])
    }
  }
  
  //recursively sort 
  if(firstHalf.length > 0 && secondHalf.length > 0){
    return [...quickSort(firstHalf), pivotPoint, ...quickSort(secondHalf)]
  } else if(firstHalf.length > 0){
    return [...quickSort(firstHalf), pivotPoint]
  } else{
    //secondHalf.length > 0
    return [pivotPoint, ...quickSort(secondHalf)]
  }
}

quickSort([1,4,2,8,345,123,43,32,5643,63,123,43,2,55,1,234,92])
//should return an array that is unchanged except for order.
````
### Problem Set
|   |  |
| :--- | :--- |
| [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) | [My Solution](https://github.com/Chanda-Abdul/leetcode/blob/master/0215.%20Kth%20Largest%20Element%20in%20an%20Array.md) | 
| [Move Zeroes](https://leetcode.com/problems/move-zeroes/) | [My Solution](https://github.com/Chanda-Abdul/leetcode/blob/master/0283.%20%F0%9F%A7%99%E2%80%8D%E2%99%80%EF%B8%8F%20Move%20Zeroes.md) | 
| [First Missing Positive](https://leetcode.com/problems/first-missing-positive/) | [My Solution](https://github.com/Chanda-Abdul/leetcode/blob/master/0041.%20First%20Missing%20Positive.md) | 
| [Sort Array By Parity](https://leetcode.com/problems/sort-array-by-parity/) | <s>[My Solution]()</s> | 
| [Sort Colors](https://leetcode.com/problems/sort-colors/) | [My Solution](https://github.com/Chanda-Abdul/leetcode/blob/master/0075.%20Sort%20Colors.md) | 
## 🔍 Merge Sort
Another common intermediate sorting algorithm is <b>merge sort</b>. Like quick sort, <b>merge sort</b> also uses a divide-and-conquer, recursive methodology to sort an array. It takes advantage of the fact that it is relatively easy to sort two arrays as long as each is sorted in the first place. But we'll start with only one array as input, so how do we get to two sorted arrays from that? Well, we can recursively divide the original input in two until we reach the base case of an array with one item. A single-item array is naturally sorted, so then we can start combining. This combination will unwind the recursive calls that split the original array, eventually producing a final sorted array of all the elements. The steps of <b>merge sort</b>, then, are:

1. Recursively split the input array in half until a sub-array with only one element is produced.
2. Merge each sorted sub-array together to produce the final sorted array.

<b>Merge sort</b> is an efficient sorting method, with time complexity of `O(nlog(n))`. This algorithm is popular because it is performant and relatively easy to implement.

````js
function merge(firstArr, secondArray) {
  //merge() which merges two sorted array into a single sorted array
  let i = 0, j = 0, mergedArr = [];
  while (i < firstArr.length && j < secondArray.length) {
    if (firstArr[i] > secondArray[j]) mergedArr.push(secondArray[j++]);
    else mergedArr.push(firstArr[i++]);
  }
  while (i < firstArr.length) {
    mergedArr.push(firstArr[i++]);
  }
  while (j < secondArray.length) {
    mergedArr.push(secondArray[j++]);
  }
  return mergedArr;
}
function mergeSort(array) {
  //base case: Array of length 1 is sorted so we return the same array back
  if (array.length == 1) return array;

  //Break down the array to half from mid into firstHalf and secondHalf
  let mid = Math.floor(array.length / 2);
  let firstHalf = mergeSort(array.slice(0, mid));
  let secondHalf = mergeSort(array.slice(mid));

  //recursively return the merged sorted array
  return merge(firstHalf, secondHalf);
}

mergeSort([1,4,2,8,345,123,43,32,5643,63,123,43,2,55,1,234,92])
//should return an array that is unchanged except for order.
````
<!-- 
### Problem Set
|   |  |
| :--- | :--- |
| [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) | [My Solution](https://github.com/Chanda-Abdul/leetcode/blob/master/0215.%20Kth%20Largest%20Element%20in%20an%20Array.md) | 
| [Move Zeroes](https://leetcode.com/problems/move-zeroes/) | [My Solution](https://github.com/Chanda-Abdul/leetcode/blob/master/0283.%20%F0%9F%A7%99%E2%80%8D%E2%99%80%EF%B8%8F%20Move%20Zeroes.md) | 
| [First Missing Positive](https://leetcode.com/problems/first-missing-positive/) | [My Solution](https://github.com/Chanda-Abdul/leetcode/blob/master/0041.%20First%20Missing%20Positive.md) | 
| [Sort Array By Parity](https://leetcode.com/problems/sort-array-by-parity/) | <s>[My Solution]()</s> | 
| [Sort Colors](https://leetcode.com/problems/sort-colors/) | [My Solution](https://github.com/Chanda-Abdul/leetcode/blob/master/0075.%20Sort%20Colors.md) |  -->
## Binary Search
Binary search is an `O(log(n))` efficiency algorithm for searching a sorted array to find an element. It operates using the following steps:
1. Find the `middle value` of a sorted array. If `value == target` `return (found it!)`.
2. If `middle value < target`, search right half of `array` in next compare.
3. If `middle value > target`, search left half of `array` in next compare.
![](https://www.geeksforgeeks.org/wp-content/uploads/Binary-Search.png)

As you can see, you are successively halving an array, which gives you the `log(n)` efficiency. For this challenge, we want you to show your work - how you got to the target value... the path you took!

  > Write a function `binarySearch` that implements the binary search algorithm on an array, returning the path you took (each middle value comparison) to find the `target` in an `array`.
  > 
  > The function takes a sorted `array` of integers and a target `value` as input. It returns an `array` containing (in-order) the `middle value` you found at each halving of the original array until you found the target `value`. The target `value` should be the last element of the returned array. If value not is found, return the string `Value Not Found`.

For example, `binarySearch([1,2,3,4,5,6,7], 5)` would return `[4,6,5]`.

For this challenge, when halving, you MUST use `Math.floor()` when doing division: `Math.floor(x/2)`. This will give a consistent, testable path.

````js
function binarySearch(searchList, value) {
  let arrayPath = [];
  let start = 0;
  let end = searchList.length - 1;
  let mid = Math.floor(end / 2);

  //if first comparison finds value
  if (searchList[mid] === value) {
    arrayPath.push(searchList[mid]);
    return arrayPath;
  }

  while (searchList[mid] !== value) {
    //add to output array
    arrayPath.push(searchList[mid]);

    //not found
    if (end < start) {
      return 'Value Not Found';
    }
    //value is in first or second half of array
    if (searchList[mid] > value) {
      end = mid - 1;
      mid = start + Math.floor((end - start) / 2);
    } else {
      //searchList[mid] < value
      start = mid + 1;
      mid = start + Math.floor((end - start) / 2);
    }
    if (searchList[mid] === value) {
      arrayPath.push(searchList[mid]);
      break;
    }
  }
  return arrayPath;
}

binarySearch([0, 1, 2, 3, 4, 5, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22,23, 49, 70], 0); 
//[13, 5, 2, 0]
binarySearch([0, 1, 2, 3, 4, 5, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22,23, 49, 70], 1); 
//[13, 5, 2, 0]
binarySearch([0, 1, 2, 3, 4, 5, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22,23, 49, 70], 2); 
//[13, 5, 2]
binarySearch([0, 1, 2, 3, 4, 5, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22,23, 49, 70], 6); 
//'Value Not Found'
binarySearch([0, 1, 2, 3, 4, 5, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22,23, 49, 70], 1); 
//[13, 5, 10]
binarySearch([0, 1, 2, 3, 4, 5, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22,23, 49, 70], 13); 
//[13]
binarySearch([0, 1, 2, 3, 4, 5, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 49, 70], 70); 
//[13, 19, 22, 49, 70]
````
<!--
 ### Problem Set 
|   |  |
| :--- | :--- |
| [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) | [My Solution](https://github.com/Chanda-Abdul/leetcode/blob/master/0215.%20Kth%20Largest%20Element%20in%20an%20Array.md) | 
| [Move Zeroes](https://leetcode.com/problems/move-zeroes/) | [My Solution](https://github.com/Chanda-Abdul/leetcode/blob/master/0283.%20%F0%9F%A7%99%E2%80%8D%E2%99%80%EF%B8%8F%20Move%20Zeroes.md) | 
| [First Missing Positive](https://leetcode.com/problems/first-missing-positive/) | [My Solution](https://github.com/Chanda-Abdul/leetcode/blob/master/0041.%20First%20Missing%20Positive.md) | 
| [Sort Array By Parity](https://leetcode.com/problems/sort-array-by-parity/) | <s>[My Solution]()</s> | 
| [Sort Colors](https://leetcode.com/problems/sort-colors/) | [My Solution](https://github.com/Chanda-Abdul/leetcode/blob/master/0075.%20Sort%20Colors.md) |  -->
