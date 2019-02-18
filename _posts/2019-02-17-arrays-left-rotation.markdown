**Arrays: Left Rotation** 

Given an array a of n integers and a number d, perform d left rotations on the array. 
Return the updated array to be printed as a single line of space-separated integers.

___

My psuedocode for this problem looks like this:

> when d equals number of left rotations

>> For d times

>>> * set variable first to the first index of the array 
>>> * delete the first index of the array
>>> * Push variable first to the end of the array

> return rotated array 

___

Code:

```
// Complete the rotLeft function below.
function rotLeft(a, d) {

    for (let i = 0; i < d; i++) {
        let first = a.shift();
        a.push(first);
    }
    return a;

}
```
