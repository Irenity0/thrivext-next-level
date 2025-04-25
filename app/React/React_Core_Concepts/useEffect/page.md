# 4. useEffect

---

React-এ `useEffect` হলো একটি হুক, যেটি component রেন্ডার হওয়ার পর বা নির্দিষ্ট কিছু state বা prop পরিবর্তিত হলে কোন কাজ চালাতে ব্যবহৃত হয়।

এটি মূলত Side Effects পরিচালনার জন্য ব্যবহৃত হয়।

👉 **Side Effect মানে:** এমন কাজ যা component-এর ভিতরে সরাসরি UI-এর রেন্ডারিং-এর অংশ নয়, যেমন:

- API Call
- Event Listener Setup
- Timer Set করা (`setTimeout`, `setInterval`)
- ডকুমেন্ট টাইটেল পরিবর্তন
- DOM এর সাথে সরাসরি কাজ করা

## 🧩 useEffect এর গঠন

```jsx
useEffect(() => {
  // কাজ যা করতে হবে
  return () => {
    // Optional: Cleanup কোড (unmount এর সময়)
  };
}, [dependency1, dependency2]);
```

## 🟡 মাউন্ট (Mount) এবং আনমাউন্ট (Unmount) ব্যাখ্যা

### 🔹 Component Mount:

যখন একটি Component প্রথমবার DOM-এ যোগ হয়, তখন বলে Mount হয়েছে।

**useEffect কখন চালাবে:** যদি dependency array খালি থাকে `[]`, তাহলে effect শুধুমাত্র প্রথমবার চলবে।

```jsx
useEffect(() => {
  console.log("Component Mounted");
}, []); // শুধুমাত্র প্রথমবার
```

### 🔹 Component Unmount:

যখন component DOM থেকে সরিয়ে ফেলা হয়, তখন তাকে বলে Unmount। এই সময় Cleanup Function চালানো হয়।

```jsx
useEffect(() => {
  const timer = setInterval(() => {
    console.log("Running...");
  }, 1000);

  return () => {
    clearInterval(timer); // Unmount হওয়ার সময় বন্ধ করে দিচ্ছি
    console.log("Component Unmounted");
  };
}, []);
```

---

## 🧪 Dependency Array-এর ব্যবহার

- `[]` 👉 শুধুমাত্র Component মাউন্ট হওয়ার সময় effect চালাবে।
- `[count]` 👉 প্রতিবার `count` পরিবর্তন হলে effect চালাবে।
- `undefined` (কিছু না দিলে) 👉 প্রতিবার রেন্ডার হওয়ার সময় effect চালাবে।

```jsx
useEffect(() => {
  console.log("Every render"); // dependency array নাই, তাই সব রেন্ডারে চালাবে
});

useEffect(() => {
  console.log("Only on mount"); // খালি array
}, []);

useEffect(() => {
  console.log("Runs when count changes");
}, [count]); // নির্দিষ্ট dependency
```

---

## ✅ বাস্তব উদাহরণ (API Call)

```jsx
import { useEffect, useState } from "react";

function User() {
  const [user, setUser] = useState(null);

  useEffect(() => {
    fetch("https://api.example.com/user")
      .then((res) => res.json())
      .then((data) => setUser(data));
  }, []); // খালি array মানে, Component মাউন্ট হলে একবারই API call হবে

  return user ? <p>{user.name}</p> : <p>Loading...</p>;
}
```

---

## 🧠 মনে রাখার মতো পয়েন্ট

| বিষয়                            | ব্যাখ্যা                                                     |
| ------------------------------- | ------------------------------------------------------------ |
| `useEffect(() => {...}, [])`    | শুধু মাউন্টের সময় চালায়                                      |
| `useEffect(() => {...})`        | প্রতিবার রেন্ডার হলে চালায়                                   |
| `useEffect(() => {...}, [dep])` | নির্দিষ্ট state বা prop পরিবর্তিত হলে চালায়                  |
| `return () => {...}`            | component unmount বা dependency পরিবর্তনের সময় cleanup চালায় |

---

## 🔚 উপসংহার:

- `useEffect` হচ্ছে Side Effects পরিচালনার প্রধান উপায় React-এ।
- এটি component lifecycle বুঝতে সাহায্য করে (Mount, Update, Unmount)।
- সঠিকভাবে dependency array ব্যবহার করলে performance উন্নত হয় এবং অপ্রয়োজনীয় effect এড়ানো যায়।
