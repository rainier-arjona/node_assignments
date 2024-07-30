# Assignment: Defining Optional Properties within Interfaces

In this assignment, you'll practice creating TypeScript interfaces to describe the shape of complex objects. You'll define optional properties within these interfaces and verify your work by running the code and logging the objects to the console.

---

**Estimated Time to Completion:** 60 mins

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives**

- Create TypeScript interfaces to describe the shape of objects
- Define optional properties within interfaces
- Ensure the objects conform to the interfaces
- Verify functionality by logging objects to the console

---

**Directions**
Create TypeScript interfaces for the following JavaScript objects. Ensure that you define optional properties where applicable. Verify your work by logging the objects to the console.

### Object 1

```tsx
const product = {
    id: 1,
    name: "Laptop",
    price: 999.99,
    description: "A high-end gaming laptop"
};
```

### Object 2

```tsx
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

### Object 3

```tsx
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

---

**Expected Output**

- Create interfaces for each object with appropriate type annotations.
- Define optional properties using the `?` syntax.
- Log the objects to the console to verify functionality.

**Hints**

- Use `?` to define optional properties in your interfaces.
- Ensure all nested objects are also strongly typed with their own interfaces.
- Log each object to the console to verify the implementation.

---

# Solutions:

### 1

```tsx
/**
 * Interface representing a product.
 * Optional properties are marked with `?`.
 */
interface Product {
    id: number;             // Required property: id of the product
    name: string;           // Required property: name of the product
    price: number;          // Required property: price of the product
    description?: string;   // Optional property: description of the product
}

/**
 * Example of a product object implementing the Product interface.
 */
const product: Product = {
    id: 1,
    name: "Laptop",
    price: 999.99,
    description: "A high-end gaming laptop" // description is provided, but it's optional
};

console.log(product); // Log the product to verify the implementation
```

### 2

```tsx
/**
 * Interface representing an address.
 * All properties are required for an address.
 */
interface Address {
    street: string;         // Required property: street name
    city: string;           // Required property: city name
    state: string;          // Required property: state name
    postalCode: string;     // Required property: postal code
}

/**
 * Interface representing a user.
 * Optional properties are marked with `?`.
 */
interface User {
    id: number;             // Required property: user ID
    username: string;       // Required property: username
    email: string;          // Required property: email address
    phone?: string;         // Optional property: phone number
    address?: Address;      // Optional property: address object
}

/**
 * Example of a user object implementing the User interface.
 */
const user: User = {
    id: 123,
    username: "techguru",
    email: "techguru@example.com",
    phone: "123-456-7890",   // phone is provided, but it's optional
    address: {               // address is provided, but it's optional
        street: "123 Tech Lane",
        city: "Techville",
        state: "TX",
        postalCode: "75001"
    }
};

console.log(user); // Log the user to verify the implementation
```

### 3

```tsx
/**
 * Interface representing an order item.
 * All properties are required for an order item.
 */
interface OrderItem {
    productId: number;      // Required property: product ID
    quantity: number;       // Required property: quantity of the product
}

/**
 * Interface representing a shipping address.
 * All properties are required for a shipping address.
 */
interface ShippingAddress {
    street: string;         // Required property: street name
    city: string;           // Required property: city name
    state: string;          // Required property: state name
    postalCode: string;     // Required property: postal code
}

/**
 * Interface representing an order.
 * Optional properties are marked with `?`.
 */
interface Order {
    orderId: number;            // Required property: order ID
    userId: number;             // Required property: user ID
    items: OrderItem[];         // Required property: array of order items
    total: number;              // Required property: total price of the order
    shippingAddress?: ShippingAddress; // Optional property: shipping address object
    status?: string;            // Optional property: status of the order
    trackingNumber?: string;    // Optional property: tracking number
}

/**
 * Example of an order object implementing the Order interface.
 */
const order: Order = {
    orderId: 456,
    userId: 123,
    items: [
        {
            productId: 1,
            quantity: 2          // quantity of product with ID 1
        },
        {
            productId: 2,
            quantity: 1          // quantity of product with ID 2
        }
    ],
    total: 1499.97,              // total price of the order
    shippingAddress: {           // shipping address is provided, but it's optional
        street: "123 Tech Lane",
        city: "Techville",
        state: "TX",
        postalCode: "75001"
    },
    status: "Shipped",           // status is provided, but it's optional
    trackingNumber: "TRACK12345" // tracking number is provided, but it's optional
};

console.log(order); // Log the order to verify the implementation
```