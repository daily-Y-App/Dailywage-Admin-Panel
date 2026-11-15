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

Income/expense records များကို admin page တွင် မပြပါ။ Password၊ screen lock၊ password reset request နှင့် password reset email စနစ်များ မပါဝင်ပါ။

## User page

User page ကို ပုံမှန်အတိုင်း တိုက်ရိုက်အသုံးပြုနိုင်ပါသည်။ Screen lock မထားပါ။ Profile tab တွင် အမည်၊ Profile Code၊ Email၊ Wage၊ OT နှင့် Avatar ကို သိမ်းနိုင်ပြီး ထို profile အချက်အလက်များကို Admin page မှ စစ်ဆေးနိုင်ပါသည်။

## Firebase ပြင်ဆင်ရန်

Realtime Database Rules တွင် admin page အတွက် `users` path ကို ဖတ်ခွင့်ရှိရန် လိုအပ်ပါသည်။ Admin page ကို PIN gate ဖြင့် ဝင်ရောက်စစ်ဆေးနိုင်ပါသည်။

## Security မှတ်ချက်

Admin page ၏ PIN gate သည် client-side static page ဖြစ်သောကြောင့် အပြည့်အဝ admin security မဟုတ်ပါ။ အမှန်တကယ် admin-only access လိုပါက Firebase Authentication custom claims နှင့် admin-only Realtime Database Rules ထည့်ရန်လိုအပ်သည်။
