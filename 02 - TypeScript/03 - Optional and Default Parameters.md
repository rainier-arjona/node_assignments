Working with Optional and Default Parameters in TypeScript Functions
# Working with Optional and Default Parameters

In this assignment, you'll practice converting JavaScript functions to TypeScript by adding appropriate type annotations and implementing optional and default parameters. Each function will increase in complexity, challenging you to apply what you've learned about TypeScript functions.

**Estimated Time to Completion:** 60 mins

**Level of Complexity:** Medium

## Instructions

1. Read through the directions below.
2. Convert the JavaScript functions to TypeScript by adding appropriate type annotations and implementing optional and default parameters as needed.
3. Submit your GitHub URL by the due date.

## Evaluation Criteria & Learning Objectives

- Convert JavaScript functions to TypeScript
- Add appropriate type annotations to function parameters and return values
- Implement optional and default parameters in TypeScript functions

## Directions

Convert the following JavaScript functions to TypeScript by adding appropriate type annotations and implementing optional and default parameters where needed. Ensure that all functions are strongly typed.

### Function 1

```typescript
function greet(name) {
    return "Hello, " + name;
}

let greeting = greet("John");
```

### Function 2

```typescript
function calculateArea(width, height) {
    if (height === undefined) {
        return width * width;
    }
    return width * height;
}

let area1 = calculateArea(5);
let area2 = calculateArea(5, 10);
```

### Function 3

```typescript
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

### Function 4

```typescript
function multiply(a, b, c) {
    if (c === undefined) {
        c = 1;
    }
    return a * b * c;
}

let result1 = multiply(2, 3);
let result2 = multiply(2, 3, 4);
```

### Function 5

```typescript
function fetchData(url, callback, method) {
     if (method === undefined) {
        method = "GET";
    }
    // Simulating an API call
    setTimeout(() => {
        callback("Data from " + url + " with method " + method);
    }, 1000);
}

fetchData("https://api.example.com", function(data) {
    console.log(data);
});
```

## Expected Output

Ensure all function parameters and return values have appropriate type annotations.
Implement optional parameters using the `?` syntax.
Implement default parameters using the `=` syntax.

## Hints

- Use `: type` to add type annotations to function parameters and return values.
- Use `?` for optional parameters.
- Use `=` for default parameters.

