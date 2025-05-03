### 🟩 12. Nullish Coalescing Operator (??)

**📘 ব্যাখ্যা:**

`??` অপারেটরটি তখন ব্যবহৃত হয় যখন আপনি চান — যদি কোনো ভেরিয়েবল `null` বা `undefined` হয়, তাহলে একটি ডিফল্ট ভ্যালু সেট হবে।

**📌 উদাহরণ:**

```tsx
const isAuthenticated = undefined;

const userName = isAuthenticated ?? "Guest"; // ✅ Only null or undefined will trigger fallback
const userName2 = isAuthenticated ? "User" : "Guest"; // ❌ Falsy values like 0, "", false will also trigger fallback

console.log(userName); // Output: Guest
console.log(userName2); // Output: Guest
```

---

### 🟩 13. Optional Chaining Operator (?.)

**📘 ব্যাখ্যা:**

অপশনাল চেইনিং অপারেটর `?.` ব্যবহার করে আমরা nested object-এর মধ্যে safely অ্যাক্সেস করতে পারি, যদি কোনো অংশ `null` বা `undefined` হয় তাহলে error না দিয়ে `undefined` রিটার্ন করে।

**📌 উদাহরণ:**

```tsx
type User = {
  name: string;
  age: number;
  address: {
    permanentAddress: string;
    presentAddress?: string;
  };
};

const user: User = {
  name: "Rafsan",
  age: 20,
  address: {
    permanentAddress: "Dhaka",
    // presentAddress নাই
  },
};

const presentAddress = user.address?.presentAddress ?? "Not available";
console.log(presentAddress); // Output: Not available
```

---

## 📝 Summary

| অপারেটর                  | কাজ                           | ব্যবহার              | ব্যতিক্রম               |
| ------------------------ | ----------------------------- | -------------------- | ----------------------- |
| `? :` (Ternary)          | If-else এর সংক্ষিপ্ত রূপ      | শর্ত ? সত্য : মিথ্যা | Simple conditions       |
| `??` (Nullish)           | null/undefined হলে fallback   | value ?? fallback    | শুধু null/undefined     |
| `?.` (Optional Chaining) | safely nested property access | obj?.prop?.subProp   | Prevents runtime errors |

### 🟩 14. Nullable Types (`string | null`)

**📘 ব্যাখ্যা:**

যখন কোনো ভেরিয়েবল `string` অথবা `null` হতে পারে, তখন তাকে nullable টাইপ বলা হয়। এটি ইউজারের ইনপুট, সার্চ বক্স বা API থেকে আসা ডেটার জন্য সাধারণ।

**📌 উদাহরণ:**

```tsx
const searchName = (value: string | null) => {
  if (value) {
    console.log("Searching");
  } else {
    console.log("There is nothing to search");
  }
};

searchName(null); // Output: There is nothing to search
```

**🧠 নোট:**

- `if (value)` — null বা empty হলে false ধরে।

---

### 🟩 15. Unknown Type এবং `typeof` চেক

**📘 ব্যাখ্যা:**

`unknown` টাইপ ব্যবহার করা হয় যখন আমরা জানি না কোনো ভেরিয়েবলের টাইপ কী। এটিকে ব্যবহার করার আগে `typeof` দিয়ে যাচাই করতে হয়।

**📌 উদাহরণ:**

```tsx
const getSpeedInMeterPerSecond = (value: unknown) => {
  if (typeof value === "number") {
    const convertedSpeed = (value * 1000) / 3600;
    console.log(`The speed is ${convertedSpeed} ms^-1`);
  } else if (typeof value === "string") {
    const [result, unit] = value.split(" ");
    const convertedSpeed = (parseFloat(result) * 1000) / 3600;
    console.log(`The speed is ${convertedSpeed} ms^-1`);
  } else {
    console.log("wrong input");
  }
};

getSpeedInMeterPerSecond(null); // Output: wrong input
```

**🧠 নোট:**

- `unknown` safer than `any` কারণ টাইপ না জানলে আগে চেক করতে হয়।
- Type narrowing এর মাধ্যমে সঠিক ব্রাঞ্চে execute হয়।

---

### 🟩 16. Never Type

**📘 ব্যাখ্যা:**

`never` টাইপ মানে এই ফাংশন **কখনোই কোনো ভ্যালু রিটার্ন করে না**। সাধারণত error throw করার সময় ব্যবহৃত হয়।

**📌 উদাহরণ:**

```tsx
const throwError = (msg: string): never => {
  throw new Error(msg);
};

throwError("mushkil se error hogaya"); // Execution stops here
```

**🧠 নোট:**

- `never` ফাংশনের পর আর কোড এক্সিকিউট হয় না।
- এটি ইউজ করা হয় error handling বা exhaustive checks এর ক্ষেত্রে।

---

## 📝 Summary Table

| টাইপ             | ব্যবহার                      | উদাহরণ                   | লক্ষ্য                    |
| ---------------- | ---------------------------- | ------------------------ | ------------------------- |
| `string \| null` | ইনপুট, ইউজার ডেটা            | `searchName(value)`      | null value handle করা     |
| `unknown`        | টাইপ না জানা object          | `typeof` চেক করে ব্যবহার | সুরক্ষিত ডেটা প্রোসেসিং   |
| `never`          | error throw বা infinite loop | `throwError("msg")`      | কখনোই কিছু রিটার্ন করে না |

---

📌 **Extra Tips:**

- সর্বদা `unknown` ভেরিয়েবল ব্যবহার করার আগে টাইপ চেক করুন।
- `never` শুধু তখনই ব্যবহার হয় যখন ফাংশন থেমে যায় (e.g. throw, infinite loop)।
