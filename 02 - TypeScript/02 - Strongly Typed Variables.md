Assignment: Utilizing Strongly Typed Variables
# Assignment: Strongly Typed Variables

In this assignment, you'll practice converting JavaScript code to TypeScript by adding appropriate type annotations and using type assertions where necessary. The goal is to ensure that all variables are strongly typed.

**Estimated Time to Completion:** 60 mins  
**Level of Complexity:** Medium

## Instructions

1. Read through the directions below.
2. Convert the provided JavaScript code snippets into TypeScript code, ensuring that all variables are strongly typed and appropriate type assertions are used.
3. Submit your GitHub URL by the due date.

## Evaluation Criteria & Learning Objectives

- Convert JavaScript code to TypeScript
- Add appropriate type annotations to variables
- Use type assertions to inform TypeScript about a variable's type when it cannot be inferred
- Ensure that all variables are strongly typed

## Directions

Convert the following JavaScript code snippets to TypeScript by adding appropriate type annotations and using type assertions where necessary. Ensure that all variables are strongly typed.

### Challenge 1

```typescript
let message = "Hello, world!";
let count = 42;
let isActive = true;

// Output results
console.log(message); // Output: Hello, world!
console.log(count); // Output: 42
console.log(isActive); // Output: true
```

### Challenge 2

```typescript
let user = {
    name: "Alice",
    age: 30
};

// Output results
console.log(user); // Output: { name: 'Alice', age: 30 }
```

### Challenge 3

```typescript
let items = ["apple", "banana", "cherry"];
let firstItem = items[0];

// Output results
console.log(items); // Output: ["apple", "banana", "cherry"]
console.log(firstItem); // Output: apple
```

### Challenge 4

```typescript
let total = 100;
let discount = 15;
let finalPrice = total - discount;

// Output results
console.log(total); // Output: 100
console.log(discount); // Output: 15
console.log(finalPrice); // Output: 85
```

### Challenge 5

```typescript
let someData = "123";
let numberData = parseInt(someData);

// Output results
console.log(someData); // Output: "123"
console.log(numberData); // Output: 123
```

**Expected Output:**

Ensure all variables have appropriate type annotations.
Use type assertions where the type cannot be inferred by TypeScript.

**Hints:**

- Use `: type` to add type annotations to variables.
- Use `as type` for type assertions when necessary.
