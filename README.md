# DailyWage Admin Panel

DailyWage Firebase Realtime Database ထဲရှိ **Profile အချက်အလက်များကိုသာ** စစ်ဆေးရန် အသုံးပြုသော admin page ဖြစ်သည်။

## Admin page မှာပြသမည့် data

- အသုံးပြုသူစုစုပေါင်း
- အမည်
- Profile Code
- Login Email (ထည့်ထားပါက)
- Avatar/Emoji
- Wage နှင့် OT
- Avatar URL
- Device registry count နှင့် profile တစ်ခုချင်းစီ၏ device ID အတို
- User တစ်ဦးချင်းစီ၏ daily wage income/expense records
- User app မှ Firebase သို့ sync လုပ်ထားသော AI chat history

Password၊ screen lock၊ password reset request နှင့် password reset email စနစ်များ မပါဝင်ပါ။

## Device registry

Main DailyWage app သည် screen, CPU cores, browser/device signals, timezone, language နှင့် canvas signal များကို hash ပြုလုပ်ပြီး Firestore `devices/{deviceId}` တွင် registry သိမ်းပါသည်။ Device ID တူပါက Admin list တွင် profile duplicate မဖြစ်အောင် တစ်ခုတည်းအဖြစ် စုစည်းပြပါသည်။ Browser/OS ပြောင်းလဲမှုများကြောင့် fingerprint သည် 100% အမြဲမတည်မြဲနိုင်သော best-effort deduplication ဖြစ်သည်။

## User page

User page ကို ပုံမှန်အတိုင်း တိုက်ရိုက်အသုံးပြုနိုင်ပါသည်။ Screen lock မထားပါ။ Profile tab တွင် အမည်၊ Profile Code၊ Email၊ Wage၊ OT နှင့် Avatar ကို သိမ်းနိုင်ပြီး ထို profile အချက်အလက်များကို Admin page မှ စစ်ဆေးနိုင်ပါသည်။

## Firebase ပြင်ဆင်ရန်

Realtime Database Rules တွင် admin page အတွက် `users` path ကို ဖတ်ခွင့်ရှိရန် လိုအပ်ပါသည်။ `users/{profileCode}` ထဲတွင် `records` နှင့် `aiChatHistory` ပါဝင်ပါသည်။ Firestore Rules တွင် `devices` collection ကို app write နှင့် admin read လုပ်နိုင်ရန် သီးခြားသတ်မှတ်ရပါမည်။ Admin page ကို PIN gate ဖြင့် ဝင်ရောက်စစ်ဆေးနိုင်ပါသည်။

## Security မှတ်ချက်

Admin page ၏ PIN gate သည် client-side static page ဖြစ်သောကြောင့် အပြည့်အဝ admin security မဟုတ်ပါ။ အမှန်တကယ် admin-only access လိုပါက Firebase Authentication custom claims နှင့် admin-only Realtime Database Rules ထည့်ရန်လိုအပ်သည်။
