### Assignment: Strongly Typed Variables

In this assignment, you'll practice converting JavaScript code to TypeScript by adding appropriate type annotations and using type assertions where necessary. The goal is to ensure that all variables are strongly typed.

**Estimated Time to Completion:** 60 mins

**Level of Complexity:** Medium

**Instructions**

1. **Read through the directions below.**
2. **Convert the provided JavaScript code snippets into TypeScript code,** ensuring that all variables are strongly typed and appropriate type assertions are used.
3. **Submit your GitHub URL by the due date.**

**Evaluation Criteria & Learning Objectives**

- **Convert JavaScript code to TypeScript:** Understand how to translate JavaScript code into TypeScript by adding type annotations and using type assertions.
- **Add appropriate type annotations to variables:** Ensure each variable has a clear and correct type specified.
- **Use type assertions to inform TypeScript about a variable's type when it cannot be inferred:** Apply `as type` where TypeScript cannot automatically infer the type.
- **Ensure that all variables are strongly typed:** Verify that every variable and function parameter has a defined type.

**Directions**

Convert the following JavaScript code snippets to TypeScript by adding appropriate type annotations and using type assertions where necessary. Ensure that all variables are strongly typed.

*Challenge 1*

```tsx

let message = "Hello, world!";
let count = 42;
let isActive = true;

// Output results
console.log(message); // Output: Hello, world!
console.log(count); // Output: 42
console.log(isActive); // Output: true

```

*Challenge 2*

```tsx

let user = {
    name: "Alice",
    age: 30
};

// Output results
console.log(user); // Output: { name: 'Alice', age: 30 }

```

*Challenge 3*

```tsx

let items = ["apple", "banana", "cherry"];
let firstItem = items[0];

// Output results
console.log(items); // Output: ["apple", "banana", "cherry"]
console.log(firstItem); // Output: apple

```

*Challenge 4*

```tsx

let total = 100;
let discount = 15;
let finalPrice = total - discount;

// Output results
console.log(total); // Output: 100
console.log(discount); // Output: 15
console.log(finalPrice); // Output: 85

```

*Challenge 5*

```tsx

let someData = "123";
let numberData = parseInt(someData);

// Output results
console.log(someData); // Output: "123"
console.log(numberData); // Output: 123

```

**Expected Output**

- Ensure all variables have appropriate type annotations.
- Use type assertions where the type cannot be inferred by TypeScript.

**Hints**

- Use `: type` to add type annotations to variables.
- Use `as type` for type assertions when necessary.