### Assignment: Union Types in TypeScript

In this assignment, you'll practice converting JavaScript code to TypeScript by adding appropriate type annotations and using union types where necessary. The goal is to ensure that all variables are strongly typed. You'll verify your application is working properly by running your code and observing the expected outputs in the console.

**Estimated Time to Completion:** 60 mins

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives**

- Understand how to use union types to allow variables to hold multiple types.

---

**Directions**

Convert the following JavaScript code snippets to TypeScript by adding appropriate type annotations and using union types where necessary. Ensure that all variables and function parameters are strongly typed. Verify your solutions by running the provided test cases.

**MVP Requirements: Typescript conversion with Union Types**

*Challenge 1: Basic Union Types*

***Task:*** Create a function that takes a parameter which can be either a string or a number. If it's a string, return its length. If it's a number, return its square.

```tsx
function getStringLengthOrSquare(value) {
    if (typeof value === 'string') {
        return value.length;
    } else if (typeof value === 'number') {
        return value * value;
    }
}

// Test cases
console.log(getStringLengthOrSquare("Hello")); // Output: 5
console.log(getStringLengthOrSquare(4));       // Output: 16

```

*Challenge 2: Union Type with Objects*

***Task:*** Create a function that takes a parameter which can be either an object with a `name` property or an object with an `age` property. If it has a `name`, return "Name: " followed by the name. If it has an `age`, return "Age: " followed by the age.

```tsx
function getInfo(value) {
    if (value.name) {
        return `Name: ${value.name}`;
    } else if (value.age) {
        return `Age: ${value.age}`;
    }
}

// Test cases
console.log(getInfo({ name: "Alice" })); // Output: Name: Alice
console.log(getInfo({ age: 30 }));       // Output: Age: 30

```

*Challenge 3: Union Type with Strings*

***Task:*** Create a union type `Color` that can be either "red", "green", or "blue". Write a function that takes a `Color` and returns a message describing the color.

```tsx
function describeColor(color) {
    switch(color) {
        case "red":
            return "The color is red.";
        case "green":
            return "The color is green.";
        case "blue":
            return "The color is blue.";
        default:
            return "Unknown color.";
    }
}

// Test cases
console.log(describeColor("red"));   // Output: "The color is red."
console.log(describeColor("green")); // Output: "The color is green."
console.log(describeColor("blue"));  // Output: "The color is blue."

```

*Challenge 4: Union Type with Arrays*

***Task:*** Create a function that takes a parameter which can be either an array of numbers or an array of strings. If it's an array of numbers, return their sum. If it's an array of strings, return their concatenation.

```tsx
function processArray(arr) {
    if (arr.length === 0) return null;

    if (typeof arr[0] === 'number') {
        return arr.reduce((acc, val) => acc + val, 0);
    } else if (typeof arr[0] === 'string') {
        return arr.join('');
    }
}

// Test cases
console.log(processArray([1, 2, 3, 4])); // Output: 10
console.log(processArray(["a", "b", "c"])); // Output: "abc"

```

*Challenge 5: Union Type with Different Return Types*

***Task:*** Write a function that takes a parameter which can be either a string, a number, or a boolean. Depending on the type, return a different value:

- If it's a string, return its length.
- If it's a number, return whether it's even or odd.
- If it's a boolean, return "yes" for true and "no" for false.

```tsx
function evaluate(value) {
    if (typeof value === 'string') {
        return value.length;
    } else if (typeof value === 'number') {
        return value % 2 === 0 ? "even" : "odd";
    } else if (typeof value === 'boolean') {
        return value ? "yes" : "no";
    }
}

// Test cases
console.log(evaluate("hello")); // Output: 5
console.log(evaluate(4));       // Output: "even"
console.log(evaluate(5));       // Output: "odd"
console.log(evaluate(true));    // Output: "yes"
console.log(evaluate(false));   // Output: "no"

```

**Expected Outputs**

- Ensure all variables have appropriate type annotations.
- Use `: type` to add type annotations to variables, function parameters, and return values.
- Use `as type` for type assertions when necessary.