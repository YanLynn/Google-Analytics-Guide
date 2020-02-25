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
  id: 'UA-XXX-X' #Tracking ID
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
ဒီမှာ vue သုံးထားတာဖြစ်တဲ့အတွက် vue analytics package သုံးပြီး event ထည့်လိုက်တာပါ။ laravel analytics ကိုသုံးမယ်ဆိုရင် GTM(google task manager) တွဲသုံးရမှာပါ။ ရိုးရိုး script သုံးသွင်းရမှာ အဆင်မပြေတဲ့အတွက် vue-analytics သ
eg.
`<script>window.dataLayer.push({
'event':  'new_subscriber',
'formLocation':  'footer'
});</script>`
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgxODkwODIwMF19
-->