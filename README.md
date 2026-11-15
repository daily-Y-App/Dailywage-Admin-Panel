# DailyWage Admin Panel

Firebase Realtime Database ထဲရှိ DailyWage user profile နှင့် avatar data ကို Profile Code ဖြင့် read-only စစ်ဆေးရန် အသုံးပြုသော admin page ဖြစ်သည်။

## အသုံးပြုနည်း

`index.html` ကို static hosting ဖြင့်ဖွင့်ပြီး Profile Code ထည့်ကာ **ရှာမည်** ကိုနှိပ်ပါ။ ပြသမည့်အချက်များမှာ အမည်၊ code၊ wage၊ OT၊ avatar အမျိုးအစား၊ ရွေးထားသော avatar၊ avatar URL၊ income/expense record အရေအတွက်နှင့် နောက်ဆုံး update ဖြစ်သည်။

Profile Code ကို URL မှလည်း ပေးနိုင်သည်။

```text
/index.html?code=EMP001
```

## Firebase Rules မှတ်ချက်

ဤစာမျက်နှာသည် client-side read-only lookup ဖြစ်သည်။ Firebase Realtime Database Rules က `users/{profileCode}` ကို read ခွင့်မပေးထားပါက data မပြနိုင်ပါ။ အများပြည်သူသို့ မဖွင့်မီ Firebase Authentication နှင့် admin-only rules ထည့်သွင်းရန် အကြံပြုသည်။

ဤ panel သည် Firebase data ကို ပြင်ခြင်း၊ ဖျက်ခြင်း မပြုပါ။
