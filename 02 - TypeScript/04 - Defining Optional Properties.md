### Assignment: Defining Optional Properties within Interfaces

In this assignment, you'll practice creating TypeScript interfaces to describe the shape of complex objects. You'll define optional properties within these interfaces and verify your work by running the code and logging the objects to the console.

**Estimated Time to Completion:** 60 mins

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives**

- **Create TypeScript interfaces to describe the shape of objects:** Develop accurate interfaces to model complex data structures.
- **Define optional properties within interfaces:** Use TypeScript's optional property syntax to handle properties that may or may not be present.
- **Ensure the objects conform to the interfaces:** Verify that objects adhere to the defined interfaces.
- **Verify functionality by logging objects to the console:** Ensure that your implementation is correct by logging the objects and checking their structure.

**Directions**

Create TypeScript interfaces for the following JavaScript objects. Ensure that you define optional properties where applicable. Verify your work by logging the objects to the console.

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

---

**Solutions**

*Solution for Object 1*

```tsx
tsxCopy code
/**
 * Interface representing a product.
 * Optional properties are marked with `?`.
 */
interface Product {
    id: number;
    name: string;
    price: number;
    description?: string; // Optional property
}

const product: Product = {
    id: 1,
    name: "Laptop",
    price: 999.99,
    description: "A high-end gaming laptop"
};

console.log(product);

```

*Solution for Object 2*

```tsx
tsxCopy code
/**
 * Interface representing an address.
 */
interface Address {
    street: string;
    city: string;
    state: string;
    postalCode: string;
}

/**
 * Interface representing a user.
 * Optional properties are marked with `?`.
 */
interface User {
    id: number;
    username: string;
    email: string;
    phone?: string; // Optional property
    address?: Address; // Optional property
}

const user: User = {
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

console.log(user);

```

*Solution for Object 3*

```tsx
tsxCopy code
/**
 * Interface representing an order item.
 */
interface OrderItem {
    productId: number;
    quantity: number;
}

/**
 * Interface representing a shipping address.
 */
interface ShippingAddress {
    street: string;
    city: string;
    state: string;
    postalCode: string;
}

/**
 * Interface representing an order.
 * Optional properties are marked with `?`.
 */
interface Order {
    orderId: number;
    userId: number;
    items: OrderItem[];
    total: number;
    shippingAddress?: ShippingAddress; // Optional property
    status?: string; // Optional property
    trackingNumber?: string; // Optional property
}

const order: Order = {
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

console.log(order);

```