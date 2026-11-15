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
- User တစ်ဦးချင်းအတွက် **Reset Email** ပို့ရန် ခလုတ်
- User က password မေ့ခလုတ်နှိပ်လျှင် Firebase ထဲသိမ်းသော reset request စာရင်း
- Admin က request ကိုစစ်ပြီး **Reset Email ပို့မည်** ကိုနှိပ်နိုင်ခြင်း

Admin page သည် user password ကို မသိမ်းပါ၊ မပြပါ။ Password ကို Firebase Authentication ကပဲ လုံခြုံစွာ စီမံပါသည်။

## User account နှင့် password recovery

DailyWage user page တွင် user အသစ်သည် Email နှင့် Password ဖြင့် account ဖန်တီးနိုင်သည်။ Password မေ့သွားပါက user screen lock မှ **Password မေ့သွားပါသလား?** ကိုနှိပ်ပါ။ Firebase `passwordResetRequests` ထဲတွင် email၊ profile code၊ အမည်နှင့် တောင်းဆိုချိန်ကိုသာ သိမ်းပါမယ်။ Admin page တွင် request ပေါ်လာပြီး Admin က **Reset Email ပို့မည်** ကိုနှိပ်လျှင် Firebase က user ၏ Email ထဲသို့ password အသစ်ထားရန် link ပို့ပေးပါမယ်။

Reset email သည် Firebase Authentication က ပို့ခြင်းဖြစ်ပြီး Admin page သို့မဟုတ် Realtime Database ထဲတွင် password ကို မသိမ်းပါ။

## Firebase Console ပြင်ဆင်ရန်

Firebase Console → **Authentication → Sign-in method → Email/Password** ကို Enable လုပ်ထားရပါမည်။ Firebase Authentication → **Templates** တွင် password-reset email စာသားကို ပြင်နိုင်သည်။ Realtime Database Rules တွင် app user profile data အတွက် လိုအပ်သော read/write permission ထည့်ထားရပါမည်။

## Security မှတ်ချက်

Admin page ၏ PIN gate သည် client-side static page ဖြစ်သောကြောင့် အပြည့်အဝ admin security မဟုတ်ပါ။ Password ကို client code, Realtime Database သို့မဟုတ် admin page ထဲတွင် မသိမ်းထားပါ။ အမှန်တကယ် admin-only access လိုပါက Firebase Authentication custom claims နှင့် admin-only Realtime Database Rules ထည့်ရန်လိုအပ်သည်။
