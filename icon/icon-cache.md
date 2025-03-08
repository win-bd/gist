## **Icon Cache রিফ্রেশ করুন**

আইকন ক্যাশ রিসেট করতে নিচের ধাপগুলো অনুসরণ করুন:

1. **Windows + R** প্রেস করে **cmd** লিখে **Ctrl + Shift + Enter** চাপ দিন (অ্যাডমিন মোডে চালু হবে)।
2. নিচের কমান্ডগুলো একে একে চালান:

   ```bash
   ie4uinit.exe -show
   taskkill /IM explorer.exe /F
   DEL /A /Q "%localappdata%\IconCache.db"
   DEL /A /F /Q "%localappdata%\Microsoft\Windows\Explorer\iconcache*"
   shutdown /r /f /t 00
   ```

3. কম্পিউটার **রিস্টার্ট** হয়ে গেলে চেক করুন Chrome-এর আইকন ঠিক হয়েছে কিনা।
