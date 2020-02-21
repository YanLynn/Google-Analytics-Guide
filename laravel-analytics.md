## **Install laravel analytics package**
Laravel google analytics package ထည့်သွင်းရာမှာ laravel 5.8 အတွက် google analytics 3.7.0 နဲ့ အထက် မှ အဆင်ပြေမှာပါ 
laravel version 5.8 အောက်ဆိုရင်လဲ အဆင်မပြေပါဘူး ။ laravel 5.8 => google analytics 3.7 ဆိုရင် ရပါပြီ
```php
- composer require spatie/laravel-analytics 3.7
```
install ပြီးသွားရင်တော့ vendor public လုပ်ပေးရပါမယ်
```php
php artisan vendor:publish --provider="Spatie\Analytics\AnalyticsServiceProvider"
```
vendor public လုပ်ပြီးရင် config/analytics.php file ဆောက်ပေးသွားပါလိမ့်မယ်

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1OTg5MjE2MDQsLTE0ODgxMjkyMzQsNT
A4NjQ5OTcxLC0yMDE0Njg5MjI0LC01NTMzMjM1MjhdfQ==
-->