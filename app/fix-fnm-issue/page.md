### 🙋‍♂️ fnm ব্যবহার করতে গিয়ে “Node version” সম্পর্কিত সমস্যা? এটা খুব সহজেই ঠিক করা যায়!

🔍 সমস্যা কী?
আপনি যদি fnm দিয়ে Node.js ভার্সন পরিবর্তন করতে চান, তাহলে এমন একটা বার্তা পেতে পারেন:

```code
error: We can't find the necessary environment variables to replace the Node version.
You should setup your shell profile to evaluate `fnm env`
```

- এই বার্তাটার মানে হলো — fnm জানে না কীভাবে আপনার সিস্টেমে Node ভার্সন বদলাবে, কারণ একটা ছোট্ট সেটআপ এখনও বাকি।

😊 ভয় নেই, সমাধান খুবই সহজ!
আপনার টার্মিনাল যেটা ব্যবহার করে (যেমন:powershell, bash, zsh, fish), সেটার কনফিগারেশন ফাইলে একটা লাইন যোগ করলেই কাজ হয়ে যাবে।

🔧 সমাধান ধাপে ধাপে:

👉 আপনি যদি PowerShell ব্যবহার করেন:
Windows-এ PowerShell ব্যবহার করলে fnm যেন স্বয়ংক্রিয়ভাবে কাজ করে, তার জন্য আপনাকে আপনার $PROFILE ফাইলে একটি লাইন যোগ করতে হবে। তবে তার আগে script execution চালু করতে হবে — এটা না করলে Windows স্ক্রিপ্ট চালাতে দেবে না।

🔐 Step 1: Execution Policy চালু করুন (শুধু একবার করতে হয়)
PowerShell খুলুন Admin হিসেবে (Start মেনু → PowerShell → Right-click → Run as Administrator)
এরপর চালান:

```bash
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

প্রম্পট আসলে Y চাপুন এবং Enter দিন।

এটা কেবল আপনার ইউজার একাউন্টের জন্য প্রযোজ্য — নিরাপদ ✅

🛠️ Step 2: PowerShell প্রোফাইল তৈরি করুন (যদি না থাকে)

```powershell
if (!(Test-Path -Path $PROFILE)) {
    New-Item -Type File -Path $PROFILE -Force
}
```

📝 Step 3: প্রোফাইল ফাইলটি খুলুন

```bash
notepad $PROFILE
```

এটা একটি নোটপ্যাড ফাইল খুলবে।

➕ Step 4: নিচের লাইনটি লিখে সেভ করুন

```bash
fnm env --use-on-cd --shell powershell | Out-String | Invoke-Expression
```

🔁 এরপর PowerShell বন্ধ করে নতুন করে খুলুন।

🧪 Step 5: টেস্ট করে দেখুন

```bash
fnm install 22.10.0
fnm use 22.10.0
node -v
```

এখন node -v চালালে Node.js-এর সঠিক ভার্সন দেখা উচিত। 🎉

✅ সংক্ষেপে:
একবার ExecutionPolicy সেট করলে ভবিষ্যতে আর লাগবে না

$PROFILE-এ লাইনটি যুক্ত থাকলে PowerShell চালু হলেই fnm কাজ করবে

Node ভার্সন ম্যানেজমেন্ট হবে স্মার্ট ও ঝামেলাহীন

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

😄 একবার সেটআপ করলেই কাজ সারাজীবনের জন্য!
এবার থেকে fnm আপনাকে Node ভার্সন ব্যবস্থাপনায় পুরো সাহায্য করবে — ঝামেলা ছাড়াই।

GitHub লিংক (setup গাইড সহ): 
[![GitHub](https://img.shields.io/badge/GitHub-fnm--setup-blue?logo=github)](https://github.com/Schniz/fnm#shell-setup)
