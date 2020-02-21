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
```php
return [
 /*
 * The view id of which you want to display data.
 */
 'view_id' => env('ANALYTICS_VIEW_ID'),
 /*
 * Path to the client secret json file. Take a look at the README of this package
 * to learn how to get this file. You can also pass the credentials as an array 
 * instead of a file path.
 */
 'service_account_credentials_json' => storage_path('app/analytics/service-account-credentials.json'),
 /*
 * The amount of minutes the Google API responses will be cached.
 * If you set this to zero, the responses won't be cached at all.
 */
 'cache_lifetime_in_minutes' => 60 * 24,
 /*
 * Here you may configure the "store" that the underlying Google_Client will
 * use to store it's data.  You may also add extra parameters that will
 * be passed on setCacheConfig (see docs for google-api-php-client).
 *
 * Optional parameters: "lifetime", "prefix"
 */
 'cache' => [
 'store' => 'file',
 ],
];
```

>***service-account-credentials.json*** =>  file ရဖို့ အတွက် google console api မှာ project တခုဆောက်ဖို့ လိုပါတယ် 

 > **[Google API’s site](https://console.developers.google.com/apis/)** <br>
 
 > Project Create ပြုလုပ်ပုံအဆင့်ဆင့်နဲ့ Key ယူပုံကို [create-google-console](google-console.md) မှာ ရှင်းပြထားပါတယ်
 
 ------------------------------------------------



:zap: Usage 
=======================
```php
use Analytics;
use Spatie\Analytics\Period;

//retrieve visitors and pageview data for the current day and the last seven days
$analyticsData = Analytics::fetchVisitorsAndPageViews(Period::days(7));
//retrieve visitors and pageviews since the 6 months ago
$analyticsData = Analytics::fetchVisitorsAndPageViews(Period::months(6));
//retrieve sessions and pageviews with yearMonth dimension since 1 year ago 
$analyticsData = Analytics::performQuery(
 Period::years(1),
 'ga:sessions',
 [
 'metrics' => 'ga:sessions, ga:pageviews',
 'dimensions' => 'ga:yearMonth'
 ]
);
```

```php
$startDate = Carbon::now()->subYear();
$endDate = Carbon::now();
Period::create($startDate, $endDate);
```

```php
$startDate = date_create($request->startDate);
$endDate = date_create($request->endDate);
```

```php
$start = Carbon::createFromFormat('Y-m-d', substr($request->startDate, 0, 10));
$end = Carbon::createFromFormat('Y-m-d', substr($request->endDate, 0, 10));
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExODY1MDcxMjIsLTU1MzY2Mjg3MSwtMT
M4ODg2MDU3NSwtMTc0ODMzNjAwNiwtMjk0MDM4MzMyLDc4MzM1
ODI0NCw3ODMzNTgyNDQsLTI0OTUwNTY0OCwyMDE0MzI1NDg1LD
EwOTg2NTE4NTEsLTc1MzEyMTkwNCwtNjI2OTUxNDE1LC0xNDg4
MTI5MjM0LDUwODY0OTk3MSwtMjAxNDY4OTIyNCwtNTUzMzIzNT
I4XX0=
-->