### Assignment: Debugging TypeScript Code

In this assignment, you'll debug TypeScript code snippets covering type annotations, type inference, function types, interfaces, and union types. Your task is to identify and fix errors to ensure the code compiles and runs correctly.

**Estimated Time to Completion:** 90 minutes

**Level of Complexity:** Medium

**Instructions:**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives:**

- Ensure that all type errors are addressed and the code compiles correctly.
- Apply correct type annotations and leverage TypeScript's type inference capabilities.
- Ensure that function parameters and return values are correctly typed and handled.
- Define and implement interfaces accurately to describe object structures.
- Use union types appropriately to handle different types of data.

---

**Directions**

Complete the debugging tasks outlined in the MVP Requirements. Each problem contains TypeScript code with specific errors related to variables, functions, interfaces, and union types. Your task is to identify and fix these errors to ensure the code compiles and runs correctly.

**MVP Requirements: Debugging Typescript code**

***1. Debugging Variables and Type Annotations***

*Problem 1:*

The following code has type errors. Fix the errors to ensure the code compiles and runs correctly.

```tsx
let username: string = 123;
let isStudent: boolean = "true";
let score: number = null;
let data: any = undefined;

console.log(username, isStudent, score, data);

```

***2. Debugging Functions and Parameters***

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

***3. Debugging Interfaces***

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

***4. Debugging Union Types***

*Problem 4:*

The following code has errors related to union types. Fix the errors.

```tsx
function printId(id: number | string) {
    console.log(id.toUpperCase());
}

printId(123);
printId("ABC123");

```

**Expected Output**

- All code snippets should compile without errors.
- Each snippet should produce the correct output based on the problem description.

**Additional Notes:**

- Pay close attention to type annotations and ensure they are used correctly.
- Test each code snippet after debugging to verify correctness.
