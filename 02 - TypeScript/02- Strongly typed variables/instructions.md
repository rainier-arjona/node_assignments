### Assignment: Strongly Typed Variables

In this assignment, you'll practice converting JavaScript code to TypeScript by adding appropriate type annotations and using type assertions where necessary. The goal is to ensure that all variables are strongly typed.

**Estimated Time to Completion:** 60 mins

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives**

- Understand how to use type assertions to inform TypeScript about a variable's type when the type cannot be inferred.

---

**Directions**

Convert the following JavaScript code snippets to TypeScript by adding appropriate type annotations and using type assertions where necessary. Ensure that all variables are strongly typed.

**MVP Requirements: JS to TypeScript Conversion**

1. Type Annotations:
    - Ensure that all variables and function parameters are explicitly typed.
    - Convert the provided JavaScript code snippets to TypeScript by adding appropriate type annotations to all variables, function parameters, and return types.

2. Type Assertions:
    - Resolve type inference issues using type assertions.
    - Use type assertions where necessary to ensure that TypeScript correctly understands the types being used, especially in cases where type inference might be ambiguous or insufficient.

3. Strong Typing:
    - Ensure that all code is strongly typed.
    - Modify the code to enforce strict type checking, ensuring that all variables, arrays, objects, and functions have well-defined and appropriate types.

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