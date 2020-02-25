**install vue analytics**
```
npm install vue-analytics
```
Start using it your Vue application
```javaScript
import Vue from 'vue'
import VueAnalytics from 'vue-analytics'

Vue.use(VueAnalytics, {
  id: 'UA-XXX-X' #Tracking ID
})
```

```javaScript
this.$ga.event({
	eventCategory:  'NewsDeatail count by category',
	eventAction:  this.newdetails[0]['cat_name'],
	eventLabel:  'NewsDeatail',
})
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyODk2MDE3ODZdfQ==
-->