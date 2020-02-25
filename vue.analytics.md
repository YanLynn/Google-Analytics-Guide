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
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzUyOTMxMjU3XX0=
-->