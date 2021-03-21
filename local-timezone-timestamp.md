# Create a Timestamp in a fixed timezone (independend of the user's local timezone)
This is useful, if you want to send timestamps in a fixed timezone, for example of your websites location, ignoring the timezone of the user.

## 1. Create Custom HTML Tag
This Tag makes sure, the dayjs javascript library is loaded. Make sure this Tag always fires before executing the javascript in the second step.
Code:
```
<script src="https://cdn.jsdelivr.net/npm/dayjs@latest/dayjs.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/dayjs@latest/plugin/utc.js"></script>
<script src="https://cdn.jsdelivr.net/npm/dayjs@latest/plugin/timezone.js"></script>
```

## 1. Create timestamp
You can either use a Custom Javascript Variable, Custom HTML Tag or any other means where you can write javascript. If you use a Custom HTML Tag, you can combine step 1 and 2 into one Tag.
Here's a code example:
```
dayjs.extend(dayjs_plugin_utc);
dayjs.extend(dayjs_plugin_timezone);
let localTime = dayjs.tz(dayjs.utc(), "Europe/Zurich");
dataLayer.push({
  "event":         "timeStamp",
  "unixTimestamp": localTime,                               // Unix Timestamp is always GMT/UTC, a local Unix timestamp doesn't exist
  "localTime":     localTime.format(),                      // local time as ISO8601 format
  "localTimeCust": localTime.format("YYYY-MM-DD_HH-mm-ss"), // local time with your own format definition
  "utcTime":       dayjs.utc().format(),                    // GMT/UTC time as ISO8601 format
  "utcTimeCust":   dayjs.utc().format("YYYY-MM-DD_HH-mm-ss")// GMT/UTC time with your own format definition
});
```

* You can change the timezone by copying the *tz Database Name* in the column here: https://en.wikipedia.org/wiki/List_of_tz_database_time_zones
* If you want to change the custom format, have a look here: https://day.js.org/docs/en/display/format


"\n default format: " + localTime +               //Unix Timestamp is always GMT/UTC, never local
"\n Unix Timestamp: " + unixTimestamp.valueOf() + //Unix Timestamp is always GMT/UTC, never local
"\n ISO8601 format: " + dayjs.utc().format() +    //GMT/UTC ISO8601 format
"\n String format : " + localTime.toString() +    //GMT/UTC
"\n ISO8601 format: " + localTime.format() +      //will show in local time
"\n Custom format : " + localTime.format("YYYY-MM-DD_HH-mm-ss [Escape Y]") //see https://day.js.org/docs/en/display/format
