## 检查日期和时间

[![chrono-badge]][chrono] [![cat-date-and-time-badge]][cat-date-and-time]

通过获取当前UTC的 [`DateTime`] ， 通过 [`Timelike`] 获取其中的小时/分钟/秒，
通过 [`Datelike`] 获取年/月/日/周。

```rust
extern crate chrono;
use chrono::{Datelike, Timelike, Utc};

fn main() {
    let now = Utc::now();

    let (is_pm, hour) = now.hour12();
    println!(
        "The current UTC time is {:02}:{:02}:{:02} {}",
        hour,
        now.minute(),
        now.second(),
        if is_pm { "PM" } else { "AM" }
    );
    println!(
        "And there have been {} seconds since midnight",
        now.num_seconds_from_midnight()
    );

    let (is_common_era, year) = now.year_ce();
    println!(
        "The current UTC date is {}-{:02}-{:02} {:?} ({})",
        year,
        now.month(),
        now.day(),
        now.weekday(),
        if is_common_era { "CE" } else { "BCE" }
    );
    println!(
        "And the Common Era began {} days ago",
        now.num_days_from_ce()
    );
}
```

[`Datelike`]: https://docs.rs/chrono/*/chrono/trait.Datelike.html
[`DateTime`]: https://docs.rs/chrono/*/chrono/struct.DateTime.html
[`Timelike`]: https://docs.rs/chrono/*/chrono/trait.Timelike.html
