## Display formatted date and time

[![chrono-badge]][chrono] [![cat-date-and-time-badge]][cat-date-and-time]

使用 [`Utc::now`] 获取并显示当前的 UTC 时间， 使用 [`DateTime::to_rfc2822`] 将其格式化为常用的 [RFC 2822]格式， 用 [`DateTime::to_rfc3339`] 格式化为 [RFC 3339] ，或者使用[`DateTime::format`] 来自定义格式化。


```rust
extern crate chrono;
use chrono::{DateTime, Utc};

fn main() {
    let now: DateTime<Utc> = Utc::now();

    println!("UTC now is: {}", now);
    println!("UTC now in RFC 2822 is: {}", now.to_rfc2822());
    println!("UTC now in RFC 3339 is: {}", now.to_rfc3339());
    println!("UTC now in a custom format is: {}", now.format("%a %b %e %T %Y"));
}
```

[`DateTime::format`]: https://docs.rs/chrono/*/chrono/struct.DateTime.html#method.format
[`DateTime::to_rfc2822`]: https://docs.rs/chrono/*/chrono/struct.DateTime.html#method.to_rfc2822
[`DateTime::to_rfc3339`]: https://docs.rs/chrono/*/chrono/struct.DateTime.html#method.to_rfc3339
[`Utc::now`]: https://docs.rs/chrono/*/chrono/offset/struct.Utc.html#method.now

[RFC 2822]: https://www.ietf.org/rfc/rfc2822.txt
[RFC 3339]: https://www.ietf.org/rfc/rfc3339.txt
