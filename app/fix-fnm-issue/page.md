### 🙋‍♂️ fnm ব্যবহার করতে গিয়ে “Node version” সম্পর্কিত সমস্যা? এটা খুব সহজেই ঠিক করা যায়!

🔍 সমস্যা কী?
আপনি যদি fnm দিয়ে Node.js ভার্সন পরিবর্তন করতে চান, তাহলে এমন একটা বার্তা পেতে পারেন:

```code
error: We can't find the necessary environment variables to replace the Node version.
You should setup your shell profile to evaluate `fnm env`
```

- এই বার্তাটার মানে হলো — fnm জানে না কীভাবে আপনার সিস্টেমে Node ভার্সন বদলাবে, কারণ একটা ছোট্ট সেটআপ এখনও বাকি।

😊 ভয় নেই, সমাধান খুবই সহজ!
আপনার টার্মিনাল যেটা ব্যবহার করে (যেমন: bash, zsh, fish), সেটার কনফিগারেশন ফাইলে একটা লাইন যোগ করলেই কাজ হয়ে যাবে।

🔧 সমাধান ধাপে ধাপে:
👉 আপনি যদি bash ব্যবহার করেন:

```bash
echo 'eval "$(fnm env)"' >> ~/.bashrc
source ~/.bashrc
```

- 👉 আপনি যদি zsh ব্যবহার করেন:

```bash
echo 'eval "$(fnm env)"' >> ~/.zshrc
source ~/.zshrc
```

- 👉 আর যদি আপনি fish ব্যবহার করেন:

```bash
fnm env | source
```

- ✅ সবকিছু ঠিকঠাক করলেন?
  টার্মিনালটা একবার বন্ধ করে আবার চালু করুন অথবা source কমান্ড দিয়ে ফাইলটা রিলোড করুন। ব্যস! এখন থেকে fnm দিয়ে Node ভার্সন বদলাতে আর কোনো সমস্যা হবে না।

- 📚 আরও জানতে চান?
  অফিসিয়াল গাইড:

```url
fnm.vercel.app
```

GitHub লিংক (setup গাইড সহ): fnm GitHub
