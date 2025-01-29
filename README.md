# Most Asked React Scenario-Based Interview Questions and Their Solutions

I found these questions on LinkedIn and thought, why not share the solutions to create a better resource for interview preparation? So, here are the most commonly asked React scenario-based interview questions and their answers.

## Q1. How to display dynamic HTML data in React?

For this question, fetching some fake product data from an API is a good approach. Here’s the complete solution:

```jsx
import { useEffect, useState } from "react";

export default function DynamicData() {
  const [data, setData] = useState([]);

  const getData = async () => {
    try {
      const response = await fetch("https://dummyjson.com/products");
      const productsJson = await response.json();
      setData(productsJson.products);
    } catch (error) {
      console.error(error);
    }
  };

  useEffect(() => {
    getData();
  }, []);

  return (
    <>
      <h1>How to display dynamic HTML data in React?</h1>
      <ul>
        {data.map((product) => (
          <li key={product.id}>{product.title}</li>
        ))}
      </ul>
    </>
  );
}
```

---
## Q2. How do you send data from a parent component to a child component in React?

For simplicity, let's render product data from an array of objects. Below is the complete code:

### **Parent Component**
```jsx
import Product from "./Product";

export default function SendDataFromParentToChild() {
  const products = [
    { id: 1, title: "Rice" },
    { id: 2, title: "Juice" },
  ];
  
  return (
    <>
      <h1>How do you send data from a parent component to a child component in React?</h1>
      {products.map((product) => (
        <Product key={product.id} data={product} />
      ))}
    </>
  );
}
```

### **Child Component (Product.js)**
```jsx
export default function Product({ data }) {
  return <p>{data.title}</p>;
}
```
Here, we pass each product as props and display the product title.

---
## Q3. How to call a parent component method from a child component in React?

### **Parent Component**
```jsx
import { useState } from "react";
import ChildComponent from "./ChildComponent";

export default function CallParentComponentMethod() {
  const [dataFromChild, setDataFromChild] = useState("");

  const handleReceiveData = (data) => {
    setDataFromChild(data);
  };

  return (
    <>
      <h1>How to call a parent component method from a child component in React?</h1>
      <p>Data received from child component: {dataFromChild}</p>
      <ChildComponent sendDataToParent={handleReceiveData} />
    </>
  );
}
```

### **Child Component**
```jsx
import { useState } from "react";

export default function ChildComponent({ sendDataToParent }) {
  const [data, setData] = useState("");

  const handleSendDataToParent = () => {
    sendDataToParent(data);
  };

  return (
    <div>
      <input type="text" value={data} onChange={(e) => setData(e.target.value)} />
      <button onClick={handleSendDataToParent}>Send Data To Parent</button>
    </div>
  );
}
```
The child component calls the parent’s function to send data.

---
## Q4. How do you access the DOM element in React?
```jsx
import { useRef } from "react";

export default function AccessDomElement() {
  const nameRef = useRef(null);

  const handleClick = () => {
    alert(`Entered Name: ${nameRef.current.value}`);
  };

  return (
    <>
      <input type="text" ref={nameRef} />
      <button onClick={handleClick}>Show Name</button>
    </>
  );
}
```

---
## Q5. How to bind an array/array of objects to a dropdown in React?

### **Using an Array**
```jsx
import { useState } from "react";

export default function Dropdowns() {
  const options = ["Apple", "Mango", "Banana", "Orange", "Grapes"];
  const [fruit, setFruit] = useState("");

  return (
    <div>
      <label>Choose Your Favorite Fruit</label>
      <select value={fruit} onChange={(e) => setFruit(e.target.value)}>
        {options.map((option, index) => (
          <option key={index} value={option}>{option}</option>
        ))}
      </select>
      <p>Your Favorite Fruit is: {fruit}</p>
    </div>
  );
}
```

### **Using an Array of Objects**
```jsx
import { useState } from "react";

export default function DropdownsWithArrayOfObjects() {
  const [fruit, setFruit] = useState("mango");
  const options = [
    { label: "Mango", value: "mango" },
    { label: "Apple", value: "apple" },
    { label: "Banana", value: "banana" },
  ];

  return (
    <div>
      <label>Choose your favorite fruit!</label>
      <select value={fruit} onChange={(e) => setFruit(e.target.value)}>
        {options.map((option) => (
          <option key={option.value} value={option.value}>{option.label}</option>
        ))}
      </select>
      <p>Your favorite fruit is: {fruit}</p>
    </div>
  );
}
```

---
## Q6. How to lazy load a component in React?

### **Component Rendering the Lazy Loaded Component**
```jsx
import React, { Suspense } from "react";

const LazyLoadedComponent = React.lazy(() => import("./LazyLoadedComponent"));

export default function Question6() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <LazyLoadedComponent />
    </Suspense>
  );
}
```

### **Lazy Loaded Component**
```jsx
export default function LazyLoadedComponent() {
  return <h1>This is a lazy-loaded component</h1>;
}
```

---
## Q7. How to display data entered by the user in another textbox?
```jsx
import { useState } from "react";

export default function Question7() {
  const [email, setEmail] = useState("");

  return (
    <div>
      <h1>How to display data entered by the user in another textbox?</h1>
      <div style={{ display: "flex", gap: "2em" }}>
        <input type="email" placeholder="Enter your email" onChange={(e) => setEmail(e.target.value)} />
        <textarea value={email} placeholder="Entered user email" readOnly />
      </div>
    </div>
  );
}
```
## Contributing

If you'd like to contribute and add more questions, follow these steps:
1. Fork the repository and edit the README.md file.
2. Make your changes and create a pull request (PR).
3. Your PR will be reviewed, and I'll merge it if everything looks good.

---

More Questions coming soon!
Happy coding & learning! 🤍

