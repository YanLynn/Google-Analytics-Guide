## **Install laravel analytics package**
Laravel google analytics package ထည့်သွင်းရာမှာ laravel 5.8 အတွက် google analytics 3.7.0 နဲ့ အထက် မှ အဆင်ပြေမှာပါ 
laravel version 5.8 အောက်ဆိုရင်လဲ အဆင်မပြေပါဘူး ။ laravel 5.8 => google analytics 3.7 ဆိုရင် ရပါပြီ <br>

![](https://img.shields.io/badge/laravel-5.8-red) ![](https://img.shields.io/badge/google--analytics-3.7-blue)
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
# laravel ရဲ့ controller မှာ use Analytics; ပြန်ခေါ်သုံးရပါမယ် 
use Spatie\Analytics\Period;
# package မှာ dateTime အတွက် ပါပြီးသားဖြစ်လို့  use Spatie\Analytics\Period;  period ကိုခေါ်သုံးရုံပါပဲ


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
input data (dateTime) နဲ့ user ရဲ့ request အပေါ်မှုတည်ပြီး analytics query တွက်ချက်တဲ့အခါ dateTime format မတူတဲ့အတွက် date_create function ကို သုံးပေးရပါမယ်
```php
$startDate = date_create($request->startDate);
$endDate = date_create($request->endDate);
```

```php
$start = Carbon::createFromFormat('Y-m-d', substr($request->startDate, 0, 10));
$end = Carbon::createFromFormat('Y-m-d', substr($request->endDate, 0, 10));
```
```php
 $response = Analytics::performQuery(
            Period::create($startDate, $endDate),
            'ga:users,ga:sessions,ga:uniqueEvents,ga:pageviewsPerSession,ga:avgSessionDuration,ga:totalEvents',
            ['dimensions' => 'ga:eventCategory,ga:eventAction,ga:eventLabel,ga:deviceCategory']
        );

         $eventReport = collect($response['rows'] ?? [])->map(function (array $dateRow) {
            return [
                'eventCategory'=> $dateRow[0],
                'eventAction'=> $dateRow[1],
                'eventLabel'=>$dateRow[2],
                'deviceCategory'=>$dateRow[3],
                'users' =>  $dateRow[4],
                'sessions' =>  $dateRow[5],
                'uniqueEvents' =>$dateRow[6],
                'pageviewsPerSession' => $dateRow[7],
                'avgSessionDuration' =>  $dateRow[8],
                'totalEvents' =>  $dateRow[9],

            ];
        });
```
>googleAnalyticsController.php (Healthcare-portal)
```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Analytics;
use Spatie\Analytics\Period;
use Carbon\Carbon;
class googleAnalyticsController extends Controller
{
    public function analytics(Request $request)
    {

        $startDate = date_create($request->startDate);
        $endDate = date_create($request->endDate);

        $start = Carbon::createFromFormat('Y-m-d', substr($request->startDate, 0, 10));
        $end = Carbon::createFromFormat('Y-m-d', substr($request->endDate, 0, 10));

        $dates = [];
        while ($start->lte($end)) {

            $dates[] = $start->copy()->format('Y-m-d');
            // $dates[] = date('F' , strtotime($date));
            // $start->addMonth();
            $start->addDay();
        }

        $browser = Analytics::fetchTopBrowsers($date);
        $mostVisitedPages = Analytics::fetchMostVisitedPages($date);
        $visitors = Analytics::fetchVisitorsAndPageViews($date);
        $total_visitors = Analytics::fetchTotalVisitorsAndPageViews($date);
        $top_referrers = Analytics::fetchTopReferrers($date);
        $analyticsData = Analytics::performQuery(
            Period::years(1),
               'ga:sessions',
               [
                   'metrics' => 'ga:sessions, ga:pageviews',
                   'dimensions' => 'ga:yearMonth,ga:country'
               ]
         );

         $response = Analytics::performQuery(
            Period::create($startDate, $endDate),
            'ga:users,ga:sessions,ga:uniqueEvents,ga:pageviewsPerSession,ga:avgSessionDuration,ga:totalEvents',
            ['dimensions' => 'ga:eventCategory,ga:eventAction,ga:eventLabel,ga:deviceCategory']
        );

         $eventReport = collect($response['rows'] ?? [])->map(function (array $dateRow) {
            return [
                'eventCategory'=> $dateRow[0],
                'eventAction'=> $dateRow[1],
                'eventLabel'=>$dateRow[2],
                'deviceCategory'=>$dateRow[3],
                'users' =>  $dateRow[4],
                'sessions' =>  $dateRow[5],
                'uniqueEvents' =>$dateRow[6],
                'pageviewsPerSession' => $dateRow[7],
                'avgSessionDuration' =>  $dateRow[8],
                'totalEvents' =>  $dateRow[9],

            ];
        });

        return response()->json([    'eventReport'=>$eventReport,
                                     'browser'=>$browser,
                                     'mostVisitedPages'=>$mostVisitedPages,
                                     'visitors'=>$visitors,
                                     'total_visitors'=>$total_visitors,
                                     'top_referrers'=>$top_referrers,
                                     'analyticsData'=>$analyticsData,
                                     
                                     ]);
    }
}

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU2ODg4MzE2NywtMTQyOTc1OTEzOCwtNT
QwNTMwNjY1LDY1NTE3Mjc0LDExOTAxMjUzODEsMzA4NDE4Mjks
LTE4OTYxOTA2OTIsLTU1MzY2Mjg3MSwtMTM4ODg2MDU3NSwtMT
c0ODMzNjAwNiwtMjk0MDM4MzMyLDc4MzM1ODI0NCw3ODMzNTgy
NDQsLTI0OTUwNTY0OCwyMDE0MzI1NDg1LDEwOTg2NTE4NTEsLT
c1MzEyMTkwNCwtNjI2OTUxNDE1LC0xNDg4MTI5MjM0LDUwODY0
OTk3MV19
-->