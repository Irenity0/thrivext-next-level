# 3. State in React

**State** হচ্ছে কোনো Component-এর ভেতরে থাকা **local data**, যেটা সময়ের সাথে পরিবর্তিত হতে পারে। React Component যখন রেন্ডার হয়, তখন সে নিজের state অনুযায়ী UI তৈরি করে।

---

## 🔹 কেন ব্যবহার করি?

React Component-এর UI সাধারণত তার নিজস্ব state-এর উপর নির্ভর করে। যখন state পরিবর্তন হয়, React আবার Component রেন্ডার করে এবং নতুন UI দেখায়।

---

## ✅ উদাহরণ:

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}
```

➡️ এখানে `count` হচ্ছে state variable, এবং `setCount` হচ্ছে সেই state পরিবর্তনের জন্য একটি update function।

---

## 📸 State কেন Snapshot হিসেবে কাজ করে?

React এ state কে বলা হয় **Snapshot**, কারণ:

- প্রতিবার যখন Component রেন্ডার হয়, সেই মুহূর্তের state এর একটি কপি (অবস্থা) নিয়ে কাজ করা হয়।
- আপনি যদি `setCount(count + 1)` করেন, তাহলে React প্রথমে একটা নতুন state value তৈরি করে, তারপর পূর্বের state এবং নতুন state-এর মধ্যে পার্থক্য দেখে Component পুনরায় রেন্ডার করে।

> এটা ঠিক যেনো React প্রতিবার component কে রেন্ডার করার সময় তার একটা “ছবি” (snapshot) তুলে রাখে, এবং সেই ছবি অনুযায়ী UI তৈরি করে।

---

## 🔄 সহজ ভাষায়:

> **"State মানে একটা Component এর মুহূর্তের অবস্থা। প্রতিবার রেন্ডার হওয়ার সময়, React সেই সময়কার State এর একটা কপি নিয়ে কাজ করে—একেই বলে Snapshot।"**

---

## 🧠 মনে রাখার মতো বিষয়:

- State শুধুমাত্র Component-এর ভেতর থেকে পরিবর্তন করা যায়।
- প্রতিবার `setState()` করলে Component রি-রেন্ডার হয়।
- প্রত্যেকবার রেন্ডার করার সময় নতুন snapshot তৈরি হয়, আগেরটা আর কাজ করে না।

---

## 🔶 State as Array

React-এ যদি একাধিক item রাখতে হয়, যেমন একটি to-do list, তাহলে array ব্যবহার করা হয়।

### ✅ উদাহরণ:

```jsx
function TodoList() {
  const [tasks, setTasks] = useState(["ঘুম", "খাওয়া"]);

  const addTask = () => {
    setTasks([...tasks, "React শেখা"]); // পুরানো array রেখে নতুনটা যোগ করছি
  };

  return (
    <div>
      {tasks.map((task, index) => (
        <p key={index}>{task}</p>
      ))}
      <button onClick={addTask}>নতুন Task যোগ করো</button>
    </div>
  );
}
```

📌 **Note**:

- `...tasks` দ্বারা আগের সমস্ত task কপি করা হয়।
- তারপর `"React শেখা"` নতুন আইটেম হিসেবে যুক্ত হয়।
- এইভাবে **immutable** ভাবে array আপডেট করা হয়।

---

## 🔶 State as Object

যখন একটি state অনেকগুলো related property ধারণ করে, তখন object ব্যবহৃত হয়।

### ✅ উদাহরণ:

```jsx
function UserProfile() {
  const [user, setUser] = useState({ name: "রাফসান", age: 25 });

  const updateName = () => {
    setUser({ ...user, name: "রাফি" }); // আগের সব তথ্য রেখে নাম পরিবর্তন
  };

  return (
    <div>
      <p>নাম: {user.name}</p>
      <p>বয়স: {user.age}</p>
      <button onClick={updateName}>নাম পরিবর্তন করো</button>
    </div>
  );
}
```

📌 **Note**:

- `...user` দিয়ে আগের সব property কপি করি।
- শুধুমাত্র `name` overwrite করি।
- 📛 যদি `...user` না দিই, তাহলে `age` হারিয়ে যাবে।

---

## 🔶 Derived State

**Derived state** হল এমন কোনো ভ্যালু যা আমরা অন্য state বা props দেখে গণনা করে থাকি।

### ✅ উদাহরণ:

```jsx
function Cart({ items }) {
  // items: [{ name: "Book", price: 100 }, { name: "Pen", price: 20 }]
  const total = items.reduce((sum, item) => sum + item.price, 0);

  return (
    <div>
      <h3>মোট দাম: {total} টাকা</h3>
    </div>
  );
}
```

📌 এখানে `total` হল **derived value**, কারণ এটা `items` থেকে হিসেব করা।

---

❌ কখন derived state আলাদা করে রাখা উচিত না?

```jsx
// ভুল পদ্ধতি:
const [total, setTotal] = useState(0);

// তারপর useEffect দিয়ে update করো:
useEffect(() => {
  setTotal(items.reduce((sum, item) => sum + item.price, 0));
}, [items]);
```

👉 এই কোড কাজ করবে ঠিকই, কিন্তু **extra state এবং effect** ব্যবহারের দরকার নেই। তাই গণনা যোগ্য মান (derived value) কখনও অতিরিক্ত করে useState তে রাখা উচিত নয়।

---

## 🧠 মনে রাখার টিপস:

| ধরন       | কখন ব্যবহার করব                  | আপডেট করার উপায়                  |
| --------- | -------------------------------- | --------------------------------- |
| Primitive | ছোট/সরল মান যেমন counter         | `setState(newValue)`              |
| Array     | Task list, notifications ইত্যাদি | `setArray([...prev, newItem])`    |
| Object    | User data, ফর্মের input গুলো     | `setObj({ ...prev, updatedKey })` |
| Derived   | অন্য state থেকে গণনা করা মান     | আলাদা করে রাখা দরকার নেই          |

---

## 🔚 উপসংহার:

**State** হলো এমন একটি শক্তিশালী ধারণা যেটা component-এর **data ও behavior** কে নিয়ন্ত্রণ করে।

✅ State সঠিকভাবে ব্যবহারের মাধ্যমে:

- Component UI **ডায়নামিক** রাখা যায়
- **Efficient** ভাবে data handle করা যায়
- **Performance** উন্নত করা যায়
