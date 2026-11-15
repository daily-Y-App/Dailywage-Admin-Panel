# DailyWage Admin Panel

DailyWage Firebase Realtime Database ထဲရှိ profile data ကို စစ်ဆေးရန် သီးသန့် admin page ဖြစ်သည်။

## ပါဝင်သောစနစ်များ

- Admin PIN နှင့် Firebase Email/Password နှစ်ဆင့် login
- Firebase `users` path မှ profile ရှိသူအရေအတွက် ပြခြင်း
- အသုံးပြုနေသူများ၏ အမည်၊ Profile Code၊ Email နှင့် avatar ပြခြင်း
- Profile Code ဖြင့် user တစ်ဦးချင်းစီ lookup လုပ်ခြင်း
- Profile အချက်အလက်ထဲမှ name, code, email, wage, OT, avatar mode နှင့် avatar URL ကိုသာ ပြခြင်း
- Firebase data ကို ပြင်ခြင်း၊ ဖျက်ခြင်း မပြုပါ

## Profile မှာ Email/Password ချိတ်နည်း

DailyWage Profile tab တွင် Login Email နှင့် Password ထည့်ပြီး **Email + Password ချိတ်မည်** ကိုနှိပ်ပါ။ Password ကို Realtime Database သို့မဟုတ် Admin page ထဲတွင် မသိမ်းပါ။ Firebase Authentication က password ကို လုံခြုံစွာ စီမံပြီး profile record ထဲတွင် email နှင့် Auth UID သာ သိမ်းသည်။

## Firebase Console ပြင်ဆင်ရန်

Firebase Console → **Authentication → Sign-in method → Email/Password** ကို Enable လုပ်ထားရပါမည်။ Realtime Database Rules တွင် admin အတွက် read permission မရှိပါက user directory ကို မဖတ်နိုင်ပါ။

## အရေးကြီးသော လုံခြုံရေးမှတ်ချက်

Admin page သည် PIN + Firebase Auth ဖြင့် login ဝင်ရသော်လည်း အများပြည်သူ static page ဖြစ်သောကြောင့် အမှန်တကယ် admin security အတွက် Firebase Authentication custom claims နှင့် admin-only Realtime Database Rules ထည့်သွင်းရန် လိုအပ်သည်။ Password ကို client code သို့မဟုတ် database ထဲတွင် မသိမ်းထားပါ။
