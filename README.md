# DailyWage Admin Panel

DailyWage Firebase Realtime Database ထဲရှိ profile data ကို စစ်ဆေးရန် အသုံးပြုသော admin page ဖြစ်သည်။

## Admin page မှာပြသမည့် data

- အသုံးပြုသူစုစုပေါင်း
- အမည်
- Profile Code
- Login Email
- Avatar/Emoji
- Wage နှင့် OT
- Avatar URL

Admin page သည် user password ကို မသိမ်းပါ၊ မပြပါ။ Password ကို Firebase Authentication ကပဲ လုံခြုံစွာ စီမံပါသည်။

## User page Screen Lock

DailyWage Profile tab တွင် Email နှင့် Password ချိတ်ပြီးနောက် user page သည် Firebase Email/Password login မအောင်မြင်မချင်း screen lock ပြပါမယ်။ Login အောင်မြင်ပြီးမှသာ ရှိပြီးသား income, expense, history, balance နှင့် profile စနစ်များကို အသုံးပြုနိုင်ပါမယ်။

Firebase Auth session ကို browser session အတွင်းသာ အသုံးပြုထားသောကြောင့် session ပြီးဆုံးပြီး ပြန်ဖွင့်လျှင် login ပြန်တောင်းပါမယ်။

## Firebase Console ပြင်ဆင်ရန်

Firebase Console → **Authentication → Sign-in method → Email/Password** ကို Enable လုပ်ထားရပါမည်။ Realtime Database Rules တွင် app user profile data အတွက် လိုအပ်သော read/write permission ထည့်ထားရပါမည်။

## Security မှတ်ချက်

Admin page ၏ PIN gate သည် client-side static page ဖြစ်သောကြောင့် အပြည့်အဝ admin security မဟုတ်ပါ။ Password ကို client code, Realtime Database သို့မဟုတ် admin page ထဲတွင် မသိမ်းထားပါ။ အမှန်တကယ် admin-only access လိုပါက Firebase Authentication custom claims နှင့် admin-only Realtime Database Rules ထည့်ရန်လိုအပ်သည်။
