**Problem**

Consider this JavaScript code snippet:

```jsx
const App = () => {
  return (
    <div className='p-6 space-y-6 max-w-md mx-auto'>
      <h1 className='text-2xl font-bold'>What is React?</h1>
      <UserList users={appState.users} />
    </div>
  );
};

export default App;
```

What is the return value of calling this function with these arguments? It's `"12"`. Did you expect that? Do you think the function author's intention was to concatenate two strings, or did they have something else in mind? Isn't it possible the author wanted to add two number values together to get the sum, resulting in `3`? A lot of guessing is involved here. While the function name suggests adding numbers, isn't concatenating also a form of "adding" things together?

However, TypeScript is here to help us with our interpretation problem. With TypeScript, we can ensure that anyone reading our code (especially ourselves two weeks later) is able to correctly understand and use our function. The same snippet with TypeScript could look like this:

```ts
function addNumbers(a: number, b: number): number {
  return a + b;
}
```

What is TypeScript telling us here? It tells us that we need to pass in numbers as arguments and that this function should return a number.

If we try to call this function with string values instead, we would get the following error:

```ts
addNumbers('1', '3');
```

`Argument of type 'string' is not assignable to parameter of type 'number'.`

So, to "make TypeScript happy" (i.e., not get errors for our code), we need to pass in values with the correct data type:

```ts
addNumbers(1, 3);
```

Of course, this function is quite easy to understand, and you might have caught the error right away. But think of a function that does something a bit more complex. Wouldn't it be a good idea to be as specific about its use cases as possible? Isn't it easier to work with a function if you know which data types it expects as input and which data type its return value will have?

TypeScript helps us write better functions. It basically has two main features for functions: a) It specifies the type of input values. b) It specifies the type of output values.

---

**Parameter Type Annotations - Input Values**

- Add type annotations to declare what types of parameters the function accepts.

```ts
function multiply(a: number, b: number) {
  return a * b;
}
```

- Arguments will be checked during build time.

```ts
add('42', 5);
// --> Error: Argument of type 'string' is not assignable to parameter of type 'number'.
```

---

**Return Type Annotations - Output Values**

```ts
function greet(): string {
  return 'Hello, World!';
}

function logDate(): void {
  console.log("It's today"); // Corrected apostrophe
}
```

You usually don't need a return type annotation because of type inference. You can use them for documentation purposes, to prevent accidental changes, or simply for personal preference. One example where explicit return types can catch bugs early is with conditionally returning values from a function:

```ts
function isOldEnough(age: number): string {
  if (age >= 18) {
    // Corrected 'number' to 'age'
    return 'You are old enough.';
  }
}
```

Do you spot the bug? If the `age` is under 18, this function will return `undefined`. This is something we might want to avoid.

So, to make TypeScript happy, we should add an `else` block:

```ts
function isOldEnough(age: number): string {
  if (age >= 18)
    return 'You are old enough.';
  } else {
    return 'You are too young.';
  }
}
```

---

**Anonymous Functions**

- When TypeScript can determine the type of parameters, they will be assigned automatically through **Contextual Typing**.

```ts
[1, 2, 3].forEach(num => num * num);

[3, 4, 5].forEach(function (num) {
  return num * num;
});
```

