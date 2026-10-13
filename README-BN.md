# GitHub Pages সেটআপ

ওয়েবসাইটে প্রতি Registration ID অনুযায়ী বক্স, Member 1 Name, Additional Fields-এর Drive লিংক, search, এক মিনিটে refresh এবং server-এ password যাচাই থাকবে। Password: xoxo। ছবির preview নেই।

## ১. Google Apps Script backend

1. নির্ধারিত Google Sheet খুলুন। Extensions → Apps Script। সম্ভব হলে script.google.com থেকে New project খুলুন। **বিদ্যমান registration/payment script মুছবেন বা বদলাবেন না**—এই directory-এর জন্য আলাদা project তৈরি করুন।
2. ZIP-এর apps-script/Code.gs-এর সব code নতুন project-এর Code.gs-এ বসান। Save করুন।
3. উপরের function dropdown থেকে setup নির্বাচন করে Run চাপুন। Google permission চাইলে Sheet-এর owner account দিয়ে অনুমতি দিন। setup শুধু প্রথমবার লাগবে।
4. Deploy → New deployment → type: Web app।
5. Execute as: Me। Who has access: Anyone। Deploy করুন। (এই endpoint public হলেও data পেতে password/session লাগে।)
6. Web app URL কপি করুন। URL শেষে /exec থাকবে। /dev URL ব্যবহার করবেন না।
7. ZIP-এর config.js খুলে PASTE_YOUR_APPS_SCRIPT_EXEC_URL_HERE-এর জায়গায় ওই URL বসান।

Sheet ID আগে থেকেই দেওয়া আছে। Spreadsheet public করার প্রয়োজন নেই; deployment owner-এর Sheet পড়ার অনুমতি লাগবে। Drive file-এর permission আলাদা—লিংক ব্যবহারকারীর জন্য খুলতে উপযুক্ত sharing থাকতে হবে।

## ২. GitHub Pages

1. GitHub → New repository → নাম application-links → Create repository।
2. Add file → Upload files। ZIP extract করে **index.html, config.js এবং .nojekyll** repository root-এ আপলোড করুন। ZIP ফাইলটাই আপলোড করবেন না। Folder-এর ভেতরে index.html রাখবেন না।
3. Commit changes।
4. Settings → Pages → Source: Deploy from a branch → Branch: main → Folder: /(root) → Save।
5. কিছুক্ষণ পরে Pages-এর URL খুলুন। Password xoxo দিয়ে ঢুকুন।

apps-script/Code.gs Google Apps Script-এ রাখবেন। GitHub-এ এটি আপলোড করার দরকার নেই। README-ও ঐচ্ছিক।

## ব্যবহার

নতুন Sheet row-এ ID, নাম ও Additional Fields-এ Drive লিংক থাকলে বক্স আসবে। একই ID-এর একাধিক Drive লিংক এক বক্সে থাকবে। পেজ খোলা ও দৃশ্যমান থাকলে প্রতি মিনিটে refresh; Refresh দিয়ে সঙ্গে সঙ্গে দেখা যাবে।

Sheet connection settings-এর Tab ID খালি রাখলে প্রথম tab পড়বে। অন্য tab চাইলে Sheet URL-এর gid সংখ্যাটি দিন। Auto detect ব্যর্থ হলে column বেছে Apply settings দিন। Column settings ওই browser-এ থাকে।

## সমস্যা হলে

- Blank/error: config.js-এ /exec URL ঠিক আছে কি না দেখুন।
- Login কাজ না করলে setup Run করেছেন কি না দেখুন। Web app access Anyone হতে হবে।
- Script বদলালে Deploy → Manage deployments → Edit → Version: New version → Deploy। একই /exec URL রাখুন।
- Sheet permission বা Apps Script quota সমস্যা হলে error দেখাবে। বড় visitor load-এ Apps Script quota প্রযোজ্য।
- পুরোনো UI দেখালে Ctrl+Shift+R চাপুন।
- Password বদলাতে Apps Script → Project Settings → Script Properties → ACCESS_PASSWORD বদলান। SESSION_SECRET বদলালে পুরোনো sessions বাতিল হবে।

## যাচাইয়ের সীমা

Source syntax ও আসল Sheet-এর sample data parsing যাচাই করা হয়েছে। আপনার Google account-এ Apps Script deploy এবং GitHub Pages চালু করার পর login/data integration যাচাই করতে হবে; এই ZIP আপনার হয়ে Google বা GitHub-এ deploy করা হয়নি। কোনো participant-এর তথ্য বা Drive লিংক ZIP-এ রাখা হয়নি।
