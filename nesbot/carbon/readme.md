An international PHP extension for DateTime.

# Example

```c#
var ctx = Context.CreateEmpty();
var self = typeof(Carbon.Carbon).GetPhpTypeInfo();

var now = Carbon.Carbon.now(ctx, self);

WriteLine("Right now is {0}", now.toDateTimeString());
WriteLine("Right now in Vancouver is {0}", Carbon.Carbon.now(ctx, self, "America/Vancouver"));  //implicit __toString()
var tomorrow = now.addDay();
var lastWeek = now.subWeek();
var nextSummerOlympics = Carbon.Carbon.createFromDate(ctx, self, 2016).Cast<Carbon.Carbon>().addYears(4);

var officialDate = now.toRfc2822String();

var howOldAmI = (int)Carbon.Carbon.createFromDate(ctx, self, 1975, 5, 21).Cast<Carbon.Carbon>().__get("age");

var noonTodayLondonTime = Carbon.Carbon.createFromTime(ctx, self, 12, 0, 0, "Europe/London");

var internetWillBlowUpOn = Carbon.Carbon.create(ctx, self, 2038, 01, 19, 3, 14, 7, "GMT");

//// Don't really want this to happen so mock now
//Carbon::setTestNow(Carbon::createFromDate(2000, 1, 1));

//// comparisons are always done in UTC
//if (Carbon::now()->gte($internetWillBlowUpOn))
//{
//    die();
//}

//// Phew! Return to normal behaviour
//Carbon::setTestNow();

//if (Carbon::now()->isWeekend())
//{
//    echo 'Party!';
//}
//// Over 200 languages (and over 500 regional variants) supported:
//echo Carbon::now()->subMinutes(2)->diffForHumans(); // '2 minutes ago'
//echo Carbon::now()->subMinutes(2)->locale('zh_CN')->diffForHumans(); // '2分钟前'
WriteLine(Carbon.Carbon.parse(ctx, self, "2019-07-23 14:51").toIso8601String().ToString()); // 'Tuesday, July 23, 2019 2:51 PM'
//echo Carbon::parse('2019-07-23 14:51')->locale('fr_FR')->isoFormat('LLLL'); // 'mardi 23 juillet 2019 14:51'

//// ... but also does 'from now', 'after' and 'before'
//// rolling up to seconds, minutes, hours, days, months, years

//$daysSinceEpoch = Carbon::createFromTimestamp(0)->diffInDays();
```