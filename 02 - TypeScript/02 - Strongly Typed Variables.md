# Assignment: Utilizing Strongly Typed Variables

In this assignment, you'll practice converting JavaScript code to TypeScript by adding appropriate type annotations and using type assertions where necessary. The goal is to ensure that all variables are strongly typed.

---

**Estimated Time to Completion:** 60 mins

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives**

- Convert JavaScript code to TypeScript
- Add appropriate type annotations to variables
- Use type assertions to inform TypeScript about a variable's type when it cannot be inferred
- Ensure that all variables are strongly typed

---

**Directions**
Convert the following JavaScript code snippets to TypeScript by adding appropriate type annotations and using type assertions where necessary. Ensure that all variables are strongly typed.

### Challenge 1

```jsx
let message = "Hello, world!";
let count = 42;
let isActive = true;

// test cases
console.log(message) // Output: Hello, world!
console.log(count) // Output: 42
console.log(isActive) //Output: true
```

### Challenge 2

```jsx
function add(a, b) {
    return a + b;
}

let sum = add(5, 10);

// test cases
console.log(sum) // Output: 15
```

### Challenge 3

```jsx
let user = {
    name: "Alice",
    age: 30
};

function getUserInfo(user) {
    return `Name: ${user.name}, Age: ${user.age}`;
}

let info = getUserInfo(user);

//test cases
console.log(info) // Output: Name: Alice, Age: 30
```

### Challenge 4

```jsx
let items = ["apple", "banana", "cherry"];
let firstItem = items[0];

// Output results
console.log(items); // Output: ["apple", "banana", "cherry"]
console.log(firstItem) // Output: apple
```

### Challenge 5

```jsx
let total = 100;
let discount = 15;
let finalPrice = total - discount;

// Output results
console.log(total)
console.log(discount)
console.log(finalPrice)
```

**Expected Output**

- Ensure all variables have appropriate type annotations.
- Use type assertions where the type cannot be inferred by TypeScript.

**Hints**

- Use `: type` to add type annotations to variables, function parameters, and return values.
- Use `as type` for type assertions when necessary.

---

Solutions:

### 1

```tsx
let message: string = "Hello, world!";
let count: number = 42;
let isActive: boolean = true;
```

2

```tsx
function add(a: number, b: number): number {
    return a + b;
}

let sum: number = add(5, 10);
```

3

```tsx
interface User {
    name: string;
    age: number;
}

let user: User = {
    name: "Alice",
    age: 30
};

function getUserInfo(user: User): string {
    return `Name: ${user.name}, Age: ${user.age}`;
}

let info: string = getUserInfo(user);
```

4

```tsx
let items: string[] = ["apple", "banana", "cherry"];
let firstItem: string = items[0];

console.log(items);
console.log(firstItem);
```

5

```tsx
let total: number = 100;
let discount: number = 15;
let finalPrice: number = total - discount;

console.log(total);
console.log(discount);
console.log(finalPrice);
```