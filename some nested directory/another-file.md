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


CSS Container Queries are a powerful new feature in web development that allow developers to style elements based on the size or characteristics of their *parent container*, rather than the global viewport size. This is a significant shift from traditional responsive design, which primarily relies on media queries that respond to the browser's viewport.

### **Why Container Queries?**

Historically, responsive design has used media queries to adapt layouts based on the overall screen size. However, this approach can be limiting for modular components. Imagine a "card" component: it might need to look different when placed in a narrow sidebar compared to when it's in a wide main content area, even if the overall screen size remains the same. Container queries solve this "component-level responsiveness" problem.

### **How They Work**

Container queries use the @container CSS rule, which is analogous to the @media rule for media queries. To make an element a "query container," you need to apply the container-type property to it.

1. container-type Property:  
   This property is applied to the parent element that you want to query.  
   * container-type: size;  
     * The container queries on both the inline-size (width) and block-size (height) of the container. This is the most common and generally recommended value.  
   * container-type: inline-size;  
     * The container queries only on the inline-size (width) of the container. This is useful when you only care about the horizontal space available.  
   * container-type: block-size;  
     * The container queries only on the block-size (height) of the container.  
   * container-type: normal;  
     * The element is not a query container (default behavior).  
2. container-name Property (Optional):  
   You can optionally give a container a name using container-name: \<name\>;. This is useful when you have nested containers or want to query a specific container by name. If not specified, the query applies to the nearest ancestor with a container-type.  
3. @container Rule:  
   This is where you define the styles that apply when the container meets certain conditions. The syntax is similar to @media:  
   @container (min-width: 400px) {  
     /\* Styles to apply when the container is at least 400px wide \*/  
   }

   @container card-container (max-width: 300px) {  
     /\* Styles for a named container 'card-container' when it's at most 300px wide \*/  
   }

### **Examples**

Let's illustrate with a common "card" component example.

**Scenario:** We have a card that needs to adjust its layout based on the available width of its parent.

**HTML Structure:**

\<div class="sidebar"\>  
  \<div class="card"\>  
    \<h3\>Product A\</h3\>  
    \<img src="https://placehold.co/100x100" alt="Product Image"\>  
    \<p\>Short description of Product A.\</p\>  
    \<button\>View Details\</button\>  
  \</div\>  
\</div\>

\<div class="main-content"\>  
  \<div class="card"\>  
    \<h3\>Product B\</h3\>  
    \<img src="https://placehold.co/100x100" alt="Product Image"\>  
    \<p\>A slightly longer description for Product B, demonstrating how text might wrap differently.\</p\>  
    \<button\>View Details\</button\>  
  \</div\>  
\</div\>

**CSS with Container Queries:**

/\* Make sidebar and main-content the query containers \*/  
.sidebar {  
  container-type: inline-size; /\* Only care about width \*/  
  width: 280px; /\* Example fixed width for sidebar \*/  
  background-color: \#f0f0f0;  
  padding: 15px;  
  border-radius: 8px;  
  margin-right: 20px;  
}

.main-content {  
  container-type: inline-size; /\* Only care about width \*/  
  flex-grow: 1; /\* Allows it to take remaining space \*/  
  background-color: \#e6ffe6;  
  padding: 20px;  
  border-radius: 8px;  
}

/\* Base styles for the card \*/  
.card {  
  border: 1px solid \#ccc;  
  padding: 10px;  
  margin-bottom: 15px;  
  display: flex;  
  flex-direction: column;  
  align-items: center;  
  text-align: center;  
  gap: 10px;  
  background-color: \#fff;  
  border-radius: 6px;  
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);  
  font-family: Arial, sans-serif;  
}

.card img {  
  max-width: 100px;  
  height: auto;  
  border-radius: 4px;  
}

.card h3 {  
  margin: 0;  
  font-size: 1.1em;  
  color: \#333;  
}

.card p {  
  font-size: 0.9em;  
  color: \#666;  
}

.card button {  
  background-color: \#007bff;  
  color: white;  
  padding: 8px 12px;  
  border: none;  
  border-radius: 4px;  
  cursor: pointer;  
  font-size: 0.9em;  
  transition: background-color 0.2s ease;  
}

.card button:hover {  
  background-color: \#0056b3;  
}

/\* Container Query for .card when its parent (.sidebar or .main-content) is at least 350px wide \*/  
@container (min-width: 350px) {  
  .card {  
    flex-direction: row; /\* Arrange items horizontally \*/  
    text-align: left;  
    align-items: flex-start;  
  }

  .card img {  
    margin-right: 15px;  
  }

  .card h3 {  
    font-size: 1.3em;  
  }

  .card p {  
    flex-grow: 1; /\* Allow description to take available space \*/  
  }  
}

/\* Example with a named container (less common for simple cases but useful for complex layouts) \*/  
.product-grid {  
  container-type: inline-size;  
  container-name: product-list;  
  display: grid;  
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));  
  gap: 20px;  
}

@container product-list (min-width: 700px) {  
  /\* When the product-list container is wider than 700px, make grid items larger \*/  
  .product-grid {  
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));  
  }  
}

In this example:

* The .sidebar and .main-content divs are set as container query parents using container-type: inline-size;.  
* The .card component inside them will adapt its layout.  
* When its parent (either .sidebar or .main-content) is at least 350px wide, the card's flex-direction changes to row, making the image and text appear side-by-side. Otherwise, they stack vertically.

### **Benefits of Container Queries**

1. **Component-Driven Responsiveness:** Components can manage their own responsiveness, making them truly encapsulated and reusable.  
2. **Improved Modularity:** Styles for a component are tied to the component itself, rather than external global media queries.  
3. **Easier Maintenance:** Changes to a component's layout only require adjusting its own container queries, reducing the risk of breaking other parts of the site.  
4. **Better Collaboration:** Designers and developers can work on components with a clearer understanding of how they will behave in different contextual sizes.

### **Conclusion**

CSS Container Queries represent a significant leap forward in responsive web design, shifting the focus from the viewport to the container. They empower developers to build more robust, flexible, and truly modular web components, leading to more maintainable and scalable front-end architectures. As browser support becomes ubiquitous, they are set to become an indispensable tool in the modern web developer's toolkit.
