 > **[Google API’s site](https://console.developers.google.com/apis/)**
  login with gmail account
```
Project  name တခု ရေးပြီး Create နိုပ်ပါ
```
![enter image description here](images/6.PNG)
```
Create နိုပ်ပြီးရင် ကျနော်တို့ Project ရဲ့ Dashboard ကို ရောက်သွားပါပြီ 
အ့ဒီမှာ google analytics ရဲ့ api ကို enable လုပ်ဖို့ပေးရမယ်
```
![enter image description here](images/7.PNG)
```
Enable apis and services ကို နိုပ်ပါပြီးရင် Search box မှာ google analytics api လို့ရိုက်ရှာပြီး enable နိုပ်ပါ
```
![enter image description here](images/8.PNG)
```
google analytics api  ကို enable လုပ်ပြီးရင် key ရယူဖို့အတွက် 
Credentials ကိုသွားပါမယ်  
create credentials ထဲက service account ကိုနိုပ်ပါ
```
![enter image description here](images/9.PNG)
```
service account တခုဆောက်ပါမယ် 
service account name ကိုကြိုက်တာပေးလို့ရပါတယ်
ကိုယ်ပေးလိုက်တဲ့ name မှ service account ID (client_email) ရပါမယ်
create ကိုနိုပ်ပါ
```
![enter image description here](images/10.PNG)
```
ဒီအဆင့် Role သတ်မှတ်ပေးရပါမယ် ကျနော်တို့က Browser အတွက်သုံးပြုမှာ ဖြစ်တဲ့အတွက် Browser ကိုရွေးပါမယ် <br>
continue နိုပ်ပါ
```
![enter image description here](images/11.PNG)
```
key ယူဖို့အတွက် Create Key ကိုနိုပ်ပါ 
type ကတော့ json format ယူမှာ ဖြစ်လို့ JSON ကို ရွေးပြီး Create နိုပ် down ဖို့အတွက် ကျလာပါလိမ့်မယ်
```
![enter image description here](images/12.PNG)

![enter image description here](images/13.PNG)
```
အောက်ပါပုံအတိုင်း json data ရလာပါလိမ့်မယ်
```
![enter image description here](images/14.PNG)
```
vendor public လုပ်ပြီးရင် config/analytics.php file ထဲမှာ
အောက်ပါ storage path အတိုင်း key file ကို ထည့်ပေးရပါမယ်
```
![enter image description here](images/16.PNG)
Service Account (client_id) ကို google analytics မှာ permission ပေးဖို့ လိုအပ်ပါသေးတယ် 
[Google Analytics account](create-googleAnalytics.md) ပြုလုပ်ပုံ
![enter image description here](images/15.PNG)
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzk1OTE4ODE4LC0xMzE5MjAxNzkzLDM1OD
AzNDAyNSwxMzI0ODgxNDIzLC0xMzAxODY3MDA4LC0xMTg5NDE5
MDcwLC00Njk0NTQ0MTcsODE1NTA2MTY1LC0yMzY5ODMwMzQsLT
E4OTA0MTY1OTYsLTQwOTc1OTMwNywxNjg1NjYyMzA3LDczMDk5
ODExNl19
-->