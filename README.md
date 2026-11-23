# DailyWage Admin Panel

DailyWage Firebase Realtime Database ထဲရှိ Profile, records, AI chat နှင့် device data ကို စစ်ဆေး/စီမံရန် အသုံးပြုသော admin page ဖြစ်သည်။

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
- Referral link/code, referral attribution, active-user activity summary နှင့် phone reward claims
- Pending/Paid/Rejected claim status၊ device/phone/self-referral fraud flags နှင့် Approve & Mark Paid/Reject controls
- User row/detail ထဲမှ confirm ပြီး Profile, records, AI chat နှင့် device registry ကို ဖျက်ခြင်း

Password၊ screen lock၊ password reset request နှင့် password reset email စနစ်များ မပါဝင်ပါ။

## Device registry

Main DailyWage app သည် screen, CPU cores, browser/device signals, timezone, language နှင့် canvas signal များကို hash ပြုလုပ်ပြီး Firestore `devices/{deviceId}` တွင် registry သိမ်းပါသည်။ Device ID တူပါက Admin list တွင် profile duplicate မဖြစ်အောင် တစ်ခုတည်းအဖြစ် စုစည်းပြပါသည်။ Browser/OS ပြောင်းလဲမှုများကြောင့် fingerprint သည် 100% အမြဲမတည်မြဲနိုင်သော best-effort deduplication ဖြစ်သည်။

## User page

User page ကို ပုံမှန်အတိုင်း တိုက်ရိုက်အသုံးပြုနိုင်ပါသည်။ Screen lock မထားပါ။ Profile tab တွင် အမည်၊ Profile Code၊ Email၊ Wage၊ OT နှင့် Avatar ကို သိမ်းနိုင်ပြီး ထို profile အချက်အလက်များကို Admin page မှ စစ်ဆေးနိုင်ပါသည်။

## Firebase ပြင်ဆင်ရန်

Realtime Database Rules တွင် admin page အတွက် `users` path ကို read နှင့် selected user အတွက် delete ခွင့်ရှိရန် လိုအပ်ပါသည်။ `users/{profileCode}` ထဲတွင် `records` နှင့် `aiChatHistory` ပါဝင်ပါသည်။ Firestore Rules တွင် `devices` collection ကို app write/admin read နှင့် delete ခွင့်ရှိရန် သီးခြားသတ်မှတ်ရပါမည်။ ဖျက်ခလုတ်သည် browser `confirm` ပြီးမှသာ request ပို့ပါသည်။

## Referral Campaign

Referral Campaign UI ကို ယခု `Dailywage-Share` repo တွင် သီးသန့်ထားပါသည်။ Home app တွင် အမြဲတမ်း Referral bottom tab မရှိတော့ဘဲ Share link သာရှိပါသည်။ Share page သည် `?code=PROFILECODE` ဖြင့် ပိုင်ရှင်၏ share page ဖွင့်နိုင်ပြီး `?ref=PROFILECODE` ဖြင့် ဝင်လာသူ၏ landing/download activity ကို Firestore `shareReferrals/{deviceId}` နှင့် `shareReferralDevices/{deviceId}` တွင် တစ်ကြိမ်သာ မှတ်တမ်းတင်ပါသည်။ Home app သည် app ထဲသို့ တိုက်ရိုက်ဝင်လာသော referral များအတွက် `referralAttributions/{referredCode}`၊ `referralDevices/{deviceId}` နှင့် `referralUsers/{profileCode}` activity summary ကို ဆက်လက် sync လုပ်ပါသည်။

Claim တစ်ခုကို `referralClaims/{referredCode}` တွင် သိမ်းပြီး ဖုန်းနံပါတ်ကို `referralPhones/{phoneId}` ဖြင့် unique reserve လုပ်ပါသည်။ Claim တစ်ကြိမ် reward သည် ၂၀฿ ဖြစ်ပြီး referrer တစ်ဦးအတွက် campaign အများဆုံး ၁၀၀฿ သတ်မှတ်ထားပါသည်။ Admin သည် Activity summary နှင့် fraud flags စစ်ပြီး ဖုန်းဘေလ်ကို အပြင်ဘက်မှ ထည့်ပြီးနောက် `Approve & Mark Paid` ကိုနှိပ်ရပါမည်။ Paid ဖြစ်သည့်အခါ `referralPayouts/{claimId}` တွင် payout audit record ထည့်ပါသည်။

Approve လုပ်ပြီးသော referral reward သည် `referralBalances/{referrerCode}` တွင် `availableBalance` အဖြစ် တိုးပါသည်။ User သည် Home app မှ ဆုငွေထုတ်ယူရန် request တင်နိုင်ပြီး request ကို `referralWithdrawals/{withdrawalId}` တွင် Pending အဖြစ် သိမ်းပါသည်။ Admin သည် ဖုန်းဘေလ်ကို အမှန်တကယ်ထည့်ပြီး `Deduct Balance & Mark Paid` ကိုနှိပ်မှသာ transaction ဖြင့် `availableBalance` မှ တောင်းခံသည့်ပမာဏကို နုတ်ပြီး Withdrawal/Payout audit record သိမ်းပါသည်။ လက်ကျန်မလုံလောက်ပါက transaction က မအောင်မြင်ဘဲ ငွေမနုတ်ပါ။

Home app မှ share လုပ်သည့် personal referral link ကို တစ်ဖက် user က ဖွင့်ပြီး Profile/device ဖြင့် app ကို အသုံးပြုသောအခါ `referralAttributions` နှင့် `referralUsers` ထဲသို့ attribution၊ device၊ app open count၊ record count၊ income/expense count၊ OT hours နှင့် last active time များ sync လုပ်ပါသည်။ Admin Panel ၏ `Referral Activity` အပိုင်းတွင် Claim မတင်သေးသော referred user များကိုလည်း စစ်ဆေးနိုင်ပါသည်။ Withdrawal မတင်မီ Home app တွင် ဖုန်းနံပါတ်နှင့် Email နှစ်ခုလုံး ထည့်ရန်လိုပြီး Admin မှ ထိုအချက်အလက်များကို စစ်ဆေးပြီးမှ လက်ကျန်နုတ်ပေးပါသည်။

Withdrawal တင်သည့် transaction တစ်ခုတည်းအတွင်း `referralWithdrawals/{withdrawalId}` နှင့် `adminNotifications/{withdrawalId}` နှစ်ခုလုံးကို ဖန်တီးပါသည်။ Share page မှတင်သော request တွင် `source: share-repo` ပါပြီး ဖုန်းနံပါတ်၊ Email၊ amount နှင့် Profile Code ပါသော Pending request သည် Admin Panel သို့ ရောက်ရှိပါသည်။ Admin မှ Paid သို့မဟုတ် Rejected လုပ်သောအခါ Notification ကို `Resolved` အဖြစ် audit trail နှင့် update လုပ်ပါသည်။

Referral data collections များ၏ production rules နမူနာကို [`firestore.rules`](./firestore.rules) တွင် ထည့်ပေးထားပါသည်။ ထို rules သည် Firebase Authentication custom claim `admin == true` ကို သုံးပါသည်။ လက်ရှိ static Admin PIN သည် UI gate သာဖြစ်ပြီး Firebase Security Rules အတွက် admin အထောက်အထား မဟုတ်ပါ။ Production တွင် Home app ကို Firebase Auth (anonymous/custom token) ဖြင့် authenticate မလုပ်မချင်း ထို rules များကို တိုက်ရိုက် deploy မလုပ်ပါနှင့်။ Client-side fingerprint/phone check သည် best-effort ဖြစ်ပြီး အမှန်တကယ် မလိမ်နိုင်အောင် server-side Cloud Function/App Check နှင့် admin authentication လိုအပ်ပါသည်။

## Security မှတ်ချက်

Admin page ၏ PIN gate သည် client-side static page ဖြစ်သောကြောင့် အပြည့်အဝ admin security မဟုတ်ပါ။ Delete/write rules ကို public client အား မဖွင့်သင့်ပါ။ အမှန်တကယ် admin-only access လိုပါက Firebase Authentication custom claims သို့မဟုတ် server-side admin endpoint နှင့် admin-only Realtime Database/Firestore Rules ထည့်ရန်လိုအပ်သည်။
