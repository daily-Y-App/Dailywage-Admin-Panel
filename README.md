# DailyWage Admin Panel

DailyWage Firebase Realtime Database ထဲရှိ profile data ကို စစ်ဆေးရန် သီးသန့် admin page ဖြစ်သည်။

## ပါဝင်သောစနစ်များ

- PIN ထည့်ပြီးမှ admin panel ကို unlock လုပ်ခြင်း
- Firebase `users` path မှ profile ရှိသူအရေအတွက် ပြခြင်း
- အသုံးပြုနေသူများ၏ အမည်၊ Profile Code နှင့် avatar ပြခြင်း
- Profile Code ဖြင့် user တစ်ဦးချင်းစီ lookup လုပ်ခြင်း
- Profile အချက်အလက်ထဲမှ name, code, wage, OT, avatar mode နှင့် avatar URL ကိုသာ ပြခြင်း
- Firebase data ကို ပြင်ခြင်း၊ ဖျက်ခြင်း မပြုပါ

## အသုံးပြုနည်း

`index.html` ကိုဖွင့်ပြီး PIN ထည့်ပါ။ Unlock ပြီးလျှင် user count နှင့် profile list ကို Firebase မှ ဖတ်ပြပါမယ်။ Profile Code ရှာဖွေရန် search box ကို အသုံးပြုနိုင်သည်။

## အရေးကြီးသော လုံခြုံရေးမှတ်ချက်

ဒီ page သည် static client-side page ဖြစ်သောကြောင့် PIN ကို browser source ကိုကြည့်ပြီး ကျော်လွှားနိုင်ပါသည်။ PIN gate သည် ရိုးရှင်းသော access filter သာဖြစ်ပြီး အမှန်တကယ် admin security မဟုတ်ပါ။ အများပြည်သူသို့ အသုံးပြုမည်ဆိုလျှင် Firebase Authentication, custom claims နှင့် admin-only Realtime Database Rules ထည့်သွင်းရန် လိုအပ်သည်။

GitHub Pages deployment workflow ကို `.github/workflows/pages.yml` တွင် ထည့်ထားသည်။
