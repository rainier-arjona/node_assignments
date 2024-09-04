### Assignment: Defining Optional Properties within Interfaces

In this assignment, you'll practice creating TypeScript interfaces to describe the shape of complex objects. You'll define optional properties within these interfaces and verify your work by running the code and logging the objects to the console.

**Estimated Time to Completion:** 60 mins

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives**

- Learn how to define optional properties within interfaces.

---

**Directions**

Create TypeScript interfaces for the following JavaScript objects. Ensure that you define optional properties where applicable. Verify your work by logging the objects to the console.

**MVP Requirements: Defining Optional Properties within Interfaces**

1. Define TypeScript Interfaces:
    - Create TypeScript interfaces to represent the provided JavaScript objects.
    - Accurately define interfaces for each object, ensuring all properties are properly typed.

2. Optional Properties:
    - Specify which properties in the interfaces are optional.
    - Use the ? syntax in TypeScript to mark properties as optional where applicable, reflecting that these properties may not always be present in the object.

3. Validation:
    - Ensure that the interfaces function correctly with the provided objects.
    - Log the objects to the console to confirm that they adhere to the defined interfaces and that the optional properties are correctly handled by TypeScript.

*Object 1*

```tsx
tsxCopy code
const product = {
    id: 1,
    name: "Laptop",
    price: 999.99,
    description: "A high-end gaming laptop"
};

```

*Object 2*

```tsx
tsxCopy code
const user = {
    id: 123,
    username: "techguru",
    email: "techguru@example.com",
    phone: "123-456-7890",
    address: {
        street: "123 Tech Lane",
        city: "Techville",
        state: "TX",
        postalCode: "75001"
    }
};

```

*Object 3*

```tsx
tsxCopy code
const order = {
    orderId: 456,
    userId: 123,
    items: [
        {
            productId: 1,
            quantity: 2
        },
        {
            productId: 2,
            quantity: 1
        }
    ],
    total: 1499.97,
    shippingAddress: {
        street: "123 Tech Lane",
        city: "Techville",
        state: "TX",
        postalCode: "75001"
    },
    status: "Shipped",
    trackingNumber: "TRACK12345"
};

```

**Expected Output**

- Create interfaces for each object with appropriate type annotations.
- Define optional properties using the `?` syntax.
- Log each object to the console to verify functionality.

**Hints**

- Use `?` to define optional properties in your interfaces.
- Ensure all nested objects are also strongly typed with their own interfaces.
- Review the provided object structures to guide your interface definitions.