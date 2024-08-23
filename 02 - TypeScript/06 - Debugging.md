### Assignment: Debugging TypeScript Code

In this assignment, you'll debug TypeScript code snippets covering type annotations, type inference, function types, interfaces, and union types. Your task is to identify and fix errors to ensure the code compiles and runs correctly.

**Estimated Time to Completion:** 90 minutes

**Level of Complexity:** Medium

**Instructions:**

1. Read through the directions below.
2. Complete the necessary debugging tasks as outlined.
3. Submit your GitHub URL with your corrected code for evaluation.

**Evaluation Criteria & Learning Objectives:**

- **Identify and correct type-related errors in TypeScript code:** Ensure that all type errors are addressed and the code compiles correctly.
- **Properly use type annotations and type inference:** Apply correct type annotations and leverage TypeScript's type inference capabilities.
- **Correctly define and use functions with typed parameters and return values:** Ensure that function parameters and return values are correctly typed and handled.
- **Properly use interfaces to describe object shapes:** Define and implement interfaces accurately to describe object structures.
- **Correctly implement union types:** Use union types appropriately to handle different types of data.

**Directions**

**1. Debugging Variables and Type Annotations**

*Problem 1:*

The following code has type errors. Fix the errors to ensure the code compiles and runs correctly.

```tsx
let username: string = 123;
let isStudent: boolean = "true";
let score: number = null;
let data: any = undefined;

console.log(username, isStudent, score, data);

```

**2. Debugging Functions and Parameters**

*Problem 2:*

The following code has errors related to function parameters and return types. Fix the errors.

```tsx
function add(a: number, b: string): number {
    return a + b;
}

function greet(name: string): number {
    return `Hello, ${name}!`;
}

console.log(add(5, "10"));
console.log(greet("Alice"));

```

**3. Debugging Interfaces**

*Problem 3:*

The following code has errors related to interface definitions. Fix the errors.

```tsx
interface Person {
    name: string;
    age?: number;
    email: string;
}

const john: Person = {
    name: "John",
    email: "john@example.com",
    age: "thirty"
};

const jane: Person = {
    name: "Jane"
};

console.log(john, jane);

```

**4. Debugging Union Types**

*Problem 4:*

The following code has errors related to union types. Fix the errors.

```tsx
function printId(id: number | string) {
    console.log(id.toUpperCase());
}

printId(123);
printId("ABC123");

```

**Expected Output for All Problems:**

- All code snippets should compile without errors.
- Each snippet should produce the correct output based on the problem description.

**Additional Notes:**

- Pay close attention to type annotations and ensure they are used correctly.
- Test each code snippet after debugging to verify correctness.

---

**Solutions**

**1. Debugging Variables and Type Annotations**

```tsx
// Fixed type annotations and assigned correct values
let username: string = "John"; // Changed from number to string
let isStudent: boolean = true; // Changed from string to boolean
let score: number = 0; // Changed from null to number (0 is a valid number)
let data: any = undefined; // No change needed; 'any' type can hold undefined

console.log(username, isStudent, score, data);

```

**2. Debugging Functions and Parameters**

```tsx
// Fixed type annotations and corrected return types
function add(a: number, b: number): number {
    return a + b; // Changed b to number type for addition
}

function greet(name: string): string {
    return `Hello, ${name}!`; // Changed return type to string
}

console.log(add(5, 10)); // Both arguments are numbers
console.log(greet("Alice")); // Correct return type string

```

**3. Debugging Interfaces**

```tsx
interface Person {
    name: string;
    age?: number; // Optional property
    email: string;
}

const john: Person = {
    name: "John",
    email: "john@example.com",
    age: 30 // Changed from string to number
};

const jane: Person = {
    name: "Jane",
    email: "jane@example.com" // Added missing required property
};

console.log(john, jane);

```

**4. Debugging Union Types**

```tsx
function printId(id: number | string) {
    if (typeof id === 'string') {
        console.log(id.toUpperCase()); // Only apply to strings
    } else {
        console.log(id); // Print number directly
    }
}

printId(123); // Should print the number
printId("ABC123"); // Should print the string in uppercase

```