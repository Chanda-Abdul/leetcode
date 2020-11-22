# Remove Interval

Given a sorted list of disjoint `intervals`, each interval `intervals[i] = [a, b]` represents the set of real numbers `x` such that `a <= x < b`.

We remove the intersections between any interval in `intervals` and the interval `toBeRemoved`.

Return a sorted list of `intervals` after all such removals.

 #

### Example 1:
#### Input: 
`intervals = [[0,2],[3,4],[5,7]], toBeRemoved = [1,6]`
#### Output: 
`[[0,1],[6,7]]`
### Example 2:
#### Input: 
`intervals = [[0,5]], toBeRemoved = [2,3]`
#### Output: 
`[[0,2],[3,5]]`
### Example 3:
#### Input: 
`intervals = [[-5,-4],[-3,-2],[1,2],[3,5],[8,9]], toBeRemoved = [-1,4]`
#### Output: 
`[[-5,-4],[-3,-2],[4,5],[8,9]]`

## Constraints:

- `1 <= intervals.length <= 10^4`
- `-10^9 <= intervals[i][0] < intervals[i][1] <= 10^9`
#### Hint #1  
Solve the problem for every interval alone.
#### Hint #2  
Divide the problem into cases according to the position of the two intervals.

## My Solution
```
function removeInterval (intervals, toBeRemoved) {
let output = []
for(let i = 0; i < intervals.length; i++) {
  if((intervals[i][0] < toBeRemoved[0]) && (intervals[i][1] < toBeRemoved[0])){
    output.push(intervals[i])
    }
  if((intervals[i][0] < toBeRemoved[0]) && (intervals[i][1] >= toBeRemoved[1])){
      output.push([intervals[i][0], toBeRemoved[0]])
  } 
  if((intervals[i][0] < toBeRemoved[0]) && (intervals[i][1] > toBeRemoved[0])){
      output.push([intervals[i][0], toBeRemoved[0]])
  }
}
return output
};
```

### Input
```
removeInterval ([[0,2],[3,4],[5,7]], [1,6])//Output: [[0,1],[6,7]]
removeInterval ([[0,5]], [2,3])//[[0,2],[3,5]]
removeInterval ([[-5,-4],[-3,-2],[1,2],[3,5],[8,9]], [-1,4])//Output: [[-5,-4],[-3,-2],[4,5],[8,9]]
```

### Output
```
[ [ 0, 1 ] ]
[ [ 0, 2 ], [ 0, 2 ] ]
[ [ -5, -4 ], [ -3, -2 ] ]
```
