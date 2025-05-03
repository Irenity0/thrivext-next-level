## 🟩 **1. ভিত্তিমূলক ডেটা টাইপ (Basic Data Types)**

### String :

```tsx
let firstName: string = "Rafsan";
```

- `string` টাইপ, শুধু স্ট্রিং মান রাখবে। এখানে `firstName` এ "Rafsan" রাখা হয়েছে।

### Number :

```tsx
let age: number = 30;
```

- `number` টাইপ, শুধুমাত্র সংখ্যা রাখবে।

### Boolean :

```tsx
let isEmployed: boolean = true;
```

- `boolean` টাইপ, `true` বা `false` মান নেয়।

### Null :

```tsx
let middleName: null = null;
```

- `null` মান বোঝায় যে কোনো মান নেই।

### Undefined :

```tsx
let address: undefined = undefined;
```

- `undefined` বোঝায় যে কোনো মান এখনো সেট করা হয়নি।

### Any :

```tsx
let d;
```

- এখানে টাইপ উল্লেখ করা হয়নি, তাই এটি `any` টাইপ হয়ে যায়। TypeScript-এ এটি নিরুৎসাহিত।

```tsx
let f: number;
```

- এটি শুধু `number` টাইপ নিতে পারবে। মান পরে দেওয়া হবে।
