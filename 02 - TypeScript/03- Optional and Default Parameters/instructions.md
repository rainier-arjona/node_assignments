### Assignment: Working with Optional and Default Parameters

In this assignment, you'll practice converting JavaScript functions to TypeScript by adding appropriate type annotations and implementing optional and default parameters. Each function will increase in complexity, challenging you to apply what you've learned about TypeScript functions.

**Estimated Time to Completion:** 60 mins

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives**

- Understand how to work with optional and default parameters in TypeScript functions.

---

**Directions**

Convert the following JavaScript functions to TypeScript by adding appropriate type annotations and implementing optional and default parameters where needed. Ensure that all functions are strongly typed.

**MVP Requirements: JavaScript to TypeScript Conversion with Optional and Default Parameters**

1. Type Annotations:
    - Explicitly define the types for function parameters, return values, and variables.
    - Convert the provided JavaScript functions to TypeScript by adding appropriate type annotations for all function parameters, return types, and variables.

2. Optional Parameters:
    - Introduce optional parameters where appropriate.
    - Implement optional parameters in functions where arguments may not always be provided. Use the ? syntax to define these optional parameters.

3. Default Parameters:
    - Set default values for parameters when necessary.
    - Implement default parameters to provide fallback values for function arguments. Ensure that these defaults are correctly annotated and handled within the function logic.

4. Strong Typing:
    - Enforce strict type checking across all functions.
    - Modify the functions to enforce strong typing, ensuring all inputs and outputs are accurately typed, and the functions are resilient to incorrect types.

*Function 1*

```tsx
function greet(name) {
    return "Hello, " + name;
}

let greeting = greet("John");

```

*Function 2*

```tsx
function calculateArea(width, height) {
    if (height === undefined) {
        return width * width;
    }
    return width * height;
}

let area1 = calculateArea(5);
let area2 = calculateArea(5, 10);

```

*Function 3*

```tsx
function createUser(name, age, email) {
    return {
        name: name,
        age: age,
        email: email === undefined ? "Not provided" : email
    };
}

let user1 = createUser("Alice", 25);
let user2 = createUser("Bob", 30, "bob@example.com");

```

*Function 4*

```tsx
function multiply(a, b, c) {
    if (c === undefined) {
        c = 1;
    }
    return a * b * c;
}

let result1 = multiply(2, 3);
let result2 = multiply(2, 3, 4);

```

*Function 5*

```tsx
function fetchData(url, callback, method) {
    if (method === undefined) {
        method = "GET";
    }
    // Simulating an API call
    setTimeout(() => {
        callback("Data from " + url + " with method " + method);
    }, 1000);
}

fetchData("<https://api.example.com>", function(data) {
    console.log(data);
});

```

**Expected Output**

- Ensure all function parameters and return values have appropriate type annotations.
- Implement optional parameters where needed.
- Set default values for parameters as required.

**Hints**

- Consider how TypeScript handles parameter types and default values.
- Reflect on how optional parameters can be defined differently compared to required ones.