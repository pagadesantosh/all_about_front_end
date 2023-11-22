## Print the duplicates in an array

**Approach Taken**

1. new Set(duplicatesArray) will output a Set with unique values
2. duplicatesArray.filter(item=> if(Set.has(item){ Set.delete(item)})), this is core logic because when a duplicate 3 or 5 or any other value is came across then it will fail the if condition and executes the else condition of return item

```js
const toFindDuplicates = (duplicatesArray) => {
  const uniqueArrayElements = new Set(duplicatesArray);
  console.log('uniqueArrayElements', uniqueArrayElements); // Set {1, 2, undefined, 5, 3, 4}

  const filteredElements = duplicatesArray
    .map((item) => {
      // every item in the array is checked with set, if it is found in the Set, it will be removed from the Set and set will become empty finally
      if (uniqueArrayElements.has(item)) {
        uniqueArrayElements.delete(item);
      } else {
        // as Set only has unique elements when the duplicate 3 or 5 item comes up it will fail the if condition and execute the else condition
        return item;
      }
    })
    .filter(Boolean);
  console.log('filteredElements', filteredElements); // [1, 3, 5]
};

const newArray = [1, 2, 1, , 5, 3, 4, 3, 5];
const duplicateElements = toFindDuplicates(newArray);
```
