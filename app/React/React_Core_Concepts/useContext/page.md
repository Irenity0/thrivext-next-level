# 7. useContext

### 🔍 **useContext কী?**

`useContext` হলো React-এর একটি Hook, যেটা দিয়ে আমরা **context API** ব্যবহার করে parent থেকে deeply nested child component এ data পাঠাতে পারি **props না পাঠিয়ে**। এর মাধ্যমে আমরা **prop drilling** (এক লেভেল থেকে আরেক লেভেলে props পাঠানোর ঝামেলা) এড়াতে পারি।

---

### 🧵 **Context API-এর কাজ কী?**

ধরুন আপনার App-এ একটা `user` নামের ডেটা আছে যেটা অনেকগুলো component-এ দরকার। আপনি যদি normal way-এ করেন, তাহলে প্রতিটা component-এ props দিয়ে সেই ডেটা পাঠাতে হবে। এতে করে কোড জটিল হয়ে পড়ে।

এই সমস্যার সমাধানে আসে **Context API**। এটি দিয়ে আপনি একবার ডেটা `provide` করবেন এবং যেকোনো component-এ গিয়ে সেটা `consume` করতে পারবেন।

---

### 🧪 **useContext এর উপাদানগুলো:**

1. **createContext()** – context তৈরি করার জন্য
2. **Context.Provider** – যেটা value প্রদান করে
3. **useContext(ContextName)** – যেটা context value read করে

---

### 🧾 **উদাহরণ সহ ব্যাখ্যা:**

```jsx
import React, { createContext, useContext } from "react";

// Step 1: Context তৈরি
const UserContext = createContext();

function App() {
  const user = "রাফসান";

  return (
    // Step 2: Provider দিয়ে value পাঠানো
    <UserContext.Provider value={user}>
      <Dashboard />
    </UserContext.Provider>
  );
}

function Dashboard() {
  return (
    <div>
      <h2>Dashboard Page</h2>
      <Profile />
    </div>
  );
}

function Profile() {
  // Step 3: যেকোনো nested component-এ useContext দিয়ে value পাওয়া
  const user = useContext(UserContext);
  return <h1>স্বাগতম, {user}</h1>;
}
```

---

### ⚙️ **এই Example-এ কী হলো?**

- `UserContext` তৈরি হলো `createContext()` দিয়ে।
- `App` component-এ `UserContext.Provider` দিয়ে `user` value `'রাফসান'` প্রদান করা হলো।
- `Profile` component এ গিয়ে `useContext(UserContext)` ব্যবহার করে value টা পাওয়া গেল — **props ছাড়াই!**

---

### ✅ **কেন useContext ব্যবহার করবেন?**

- অনেক nested component-এর মধ্যেও ডেটা সহজে শেয়ার করতে পারবেন
- কোড clean ও readable হবে
- prop drilling এড়ানো যাবে
- যেকোনো global data (user info, theme, language) শেয়ার করার জন্য উপযুক্ত

---

### 🧠 **Bonus: যখন useContext না ব্যবহার করাই ভালো**

- যদি ডেটা কেবল কাছাকাছি component-এর মধ্যে প্রয়োজন হয়, তাহলে সাধারণ props ই যথেষ্ট।
- বড় অ্যাপে global state management এর জন্য Redux, Zustand বা Jotai বেশি উপযোগী হতে পারে।
