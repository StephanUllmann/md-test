# reduce()


The `.reduce()` method in JavaScript is a powerful higher-order function that processes each element in an array to produce a single cumulative value.

It is used to execute a reducer function on each element of the array, which results in a single output value.

This method is very versatile and can be used for a variety of tasks such as transforming data, accumulating values, aggregating data, and more.

### Characteristics of `.reduce()`

- **Flexibility**: Can perform almost any type of aggregation operation.
- **Non-mutating**: Does not alter the original array unless intentionally done so inside the callback.
- **Execution**: The function reduces the array to a single value, processing each element sequentially and combining it with the result of the previous operations.

### Practical Use Cases

- **Data transformation**: Transforming an array of objects into a different format.
- **Summation**: Summing up numbers in an array.
- **Counting occurrences**: Counting instances of values in an object.

//
[https://playground.wbscod.in/static/javascript-arrays-ii/7](https://playground.wbscod.in/static/javascript-arrays-ii/7)
//

```javascript
// Array of numbers
const numbers = [1, 2, 3, 4, 5];

console.info('Sum of numbers:');
const sum = numbers.reduce((acc, number) => acc + number, 0);
console.log('Sum: ', sum); // Output: 15

// Array of objects representing people
const people = [
  { name: 'Alice', age: 25 },
  { name: 'Bob', age: 30 },
  { name: 'Carol', age: 17 },
];

console.info('Average age of people:');
const averageAge = people.reduce((acc, person, index, array) => {
  acc += person.age;
  if (index === array.length - 1) {
    return acc / array.length; // return average
  }
  return acc;
}, 0);
console.log('Average Age: ', averageAge); // Output: 24

// Counting occurrences of values
const items = ['apple', 'banana', 'apple', 'orange', 'banana', 'banana'];

console.info('Counting occurrences of each fruit:');
const counts = items.reduce((acc, item) => {
  acc[item] = (acc[item] || 0) + 1;
  return acc;
}, {});
console.log('Counts:', counts); // Output: { apple: 2, banana: 3, orange: 1 }

// Transforming array data
const products = [
  { id: 1, price: 10 },
  { id: 2, price: 15 },
  { id: 3, price: 20 },
];

console.info('Total price of all products:');
const totalPrice = products.reduce((acc, product) => acc + product.price, 0);
console.log('Total Price: ', totalPrice); // Output: 45
```
