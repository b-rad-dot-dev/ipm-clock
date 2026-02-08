IPM Clock (`ipm-clock`)

Displays current time with timezone support and customizable label.

**Features:**
- Real-time clock updates every second
- Timezone support for world clocks
- Configurable 12/24-hour format
- Optional date display
- Optional seconds display

**Config:**

```json
{
  "name": "ipm-clock",
  "width": 1,
  "height": 1,
  "x": 0,
  "y": 0,
  "config": {
    "label": "Local",
    "timezone": "America/Los_Angeles",
    "use24Hour": true,
    "showSeconds": true,
    "showDate": true
  }
}
```

**Properties:**
- `label` - Text label displayed above the clock (e.g., "Local", "NYC", "Tokyo")
- `timezone` - IANA timezone name (e.g., "America/New_York", "Europe/London", "Asia/Tokyo")
    - If omitted, uses system timezone
    - See [IANA timezone list](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)
- `use24Hour` - Boolean, true for 24-hour format, false for 12-hour AM/PM (default: true)
    - Ignored if `timeFormat` is specified
- `showSeconds` - Boolean, whether to show seconds (default: true)
    - Ignored if `timeFormat` is specified
- `showDate` - Boolean, whether to show the date below the time (default: true)
- `timeFormat` - Custom time format string (optional, overrides use24Hour and showSeconds)
- `dateFormat` - Custom date format string (optional)

**Time Format Tokens:**
- `HH` - Hour in 24-hour format, 2-digit (00-23)
- `H` - Hour in 24-hour format, no padding (0-23)
- `hh` - Hour in 12-hour format, 2-digit (01-12)
- `h` - Hour in 12-hour format, no padding (1-12)
- `mm` - Minutes, 2-digit (00-59)
- `m` - Minutes, no padding (0-59)
- `ss` - Seconds, 2-digit (00-59)
- `s` - Seconds, no padding (0-59)
- `A` - AM/PM uppercase
- `a` - am/pm lowercase

**Date Format Tokens:**
- `YYYY` - 4-digit year (e.g., 2026)
- `YY` - 2-digit year (e.g., 26)
- `MMMM` - Full month name (e.g., January)
- `MMM` - Short month name (e.g., Jan)
- `MM` - Month number, 2-digit (01-12)
- `M` - Month number, no padding (1-12)
- `DD` - Day of month, 2-digit (01-31)
- `D` - Day of month, no padding (1-31)
- `dddd` - Full weekday name (e.g., Monday)
- `ddd` - Short weekday name (e.g., Mon)

**Format Examples:**

```json
{
  "name": "ipm-clock",
  "config": {
    "label": "Custom Format",
    "timezone": "America/Los_Angeles",
    "timeFormat": "h:mm:ss A",
    "dateFormat": "ddd, MMM D, YYYY"
  }
}
```

This would display:
```
CUSTOM FORMAT
2:45:30 PM
Fri, Feb 7, 2026
```

Other useful formats:
- `"HH:mm"` → 14:45 (24-hour, no seconds)
- `"h:mm A"` → 2:45 PM (12-hour, no seconds)
- `"HH:mm:ss"` → 14:45:30 (24-hour with seconds)
- `"MM/DD/YYYY"` → 02/07/2026
- `"DD/MM/YYYY"` → 07/02/2026
- `"YYYY-MM-DD"` → 2026-02-07
- `"dddd, MMMM D"` → Friday, February 7

**Multiple Clocks:**
You can add the same module multiple times with different timezones:

```json
{
  "modules": [
    {
      "name": "ipm-clock",
      "width": 1,
      "height": 1,
      "x": 0,
      "y": 0,
      "config": {
        "label": "Seattle",
        "timezone": "America/Los_Angeles"
      }
    },
    {
      "name": "ipm-clock",
      "width": 1,
      "height": 1,
      "x": 1,
      "y": 0,
      "config": {
        "label": "New York",
        "timezone": "America/New_York"
      }
    },
    {
      "name": "ipm-clock",
      "width": 1,
      "height": 1,
      "x": 2,
      "y": 0,
      "config": {
        "label": "Tokyo",
        "timezone": "Asia/Tokyo"
      }
    }
  ]
}
```