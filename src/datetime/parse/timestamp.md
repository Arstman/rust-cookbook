## 日期与UNIX时间戳相互转换
[![chrono-badge]][chrono] [![cat-date-and-time-badge]][cat-date-and-time]

使用 [`NaiveDateTime::timestamp`] 把由 [`NaiveDate::from_ymd`] 和 [`NaiveTime::from_hms`] 指定的日期转换为[UNIX timestamp] 时间戳。

然后使用 [`NaiveDateTime::from_timestamp`] 计算 January 1, 1970 0:00:00 UTC 起十亿秒之后的日期。

```rust
extern crate chrono;

use chrono::{NaiveDate, NaiveDateTime};

fn main() {
    let date_time: NaiveDateTime = NaiveDate::from_ymd(2017, 11, 12).and_hms(17, 33, 44);
    println!(
        "Number of seconds between 1970-01-01 00:00:00 and {} is {}.",
        date_time, date_time.timestamp());

    let date_time_after_a_billion_seconds = NaiveDateTime::from_timestamp(1_000_000_000, 0);
    println!(
        "Date after a billion seconds since 1970-01-01 00:00:00 was {}.",
        date_time_after_a_billion_seconds);
}
```

[`NaiveDate::from_ymd`]: https://docs.rs/chrono/*/chrono/naive/struct.NaiveDate.html#method.from_ymd
[`NaiveDateTime::from_timestamp`]: https://docs.rs/chrono/*/chrono/naive/struct.NaiveDateTime.html#method.from_timestamp
[`NaiveDateTime::timestamp`]: https://docs.rs/chrono/*/chrono/naive/struct.NaiveDateTime.html#method.timestamp
[`NaiveTime::from_hms`]: https://docs.rs/chrono/*/chrono/naive/struct.NaiveTime.html#method.from_hms

[UNIX timestamp]: https://en.wikipedia.org/wiki/Unix_time
