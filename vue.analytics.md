**install vue analytics**
```
npm install vue-analytics
```
Start using it your Vue application <br>
app.js မှာ ထည့်ပေးရမယ့် script ပါ
```javaScript
import Vue from 'vue'
import VueAnalytics from 'vue-analytics'

Vue.use(VueAnalytics, {
  id: 'UA-XXX-X' #Tracking-ID
})
```
event ထည့်နည်း
```javaScript
this.$ga.event({
	eventCategory:  'NewsDeatail count by category',
	eventAction:  this.newdetails[0]['cat_name'],
	eventLabel:  'NewsDeatail',
})
```
laravel analytics နဲ့လဲ event ထည့်လို့ရပါတယ် 
ဒီမှာ vue သုံးထားတာဖြစ်တဲ့အတွက် vue analytics package သုံးပြီး event ထည့်လိုက်တာပါ။ laravel analytics ကိုသုံးမယ်ဆိုရင် GTM(google task manager) တွဲသုံးရမှာပါ။ ရိုးရိုး script သုံးသွင်းရမှာ အဆင်မပြေတဲ့အတွက် vue-analytics သုံးခြင်းဖြစ်ပါတယ်
eg.
```javaScript
<script>
	window.dataLayer.push({
	'event':  'new_subscriber',
	'formLocation':  'footer'
	});
</script>
```


Google Analytics, Google console , laravel-analytics နှင့် vue-analytics တို့ကို အခုမှစတင်အသုံးပြုတဲ့အတွက်ကြောင့် အမှားတွေလဲ ပါကောင်းပါနိုင်ပါတယ်၊ အဆင်မပြေတာရှိရင်လဲ ပြောပြပေးပါ။ လွဲနေတာရှိရင်လဲ ပြောပြပေးပါ။ :boy:
<br>
မှတ်ချက်။ ။ git .md format များကို stackedit သုံးပြီးရေးထားပါတယ် <br>
https://stackedit.io/
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTE2MzUzMzU4XX0=
-->