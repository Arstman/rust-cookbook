## 测量两段代码之间的经过时间

[![std-badge]][std] [![cat-time-badge]][cat-time]

用 [`time::Instant::elapsed`] 测量从 [`time::Instant::now`]开始的时长。

调用 [`time::Instant::elapsed`] 会返回 [`time::Duration`] ，本例末尾我们会将其打印出来。
此方法不会更改或重置 [`time::Instant`] 对象。

```rust
use std::time::{Duration, Instant};
# use std::thread;
#
# fn expensive_function() {
#     thread::sleep(Duration::from_secs(1));
# }

fn main() {
    let start = Instant::now();
    expensive_function();
    let duration = start.elapsed();

    println!("Time elapsed in expensive_function() is: {:?}", duration);
}
```

[`time::Duration`]: https://doc.rust-lang.org/std/time/struct.Duration.html
[`time::Instant::elapsed`]: https://doc.rust-lang.org/std/time/struct.Instant.html#method.elapsed
[`time::Instant::now`]: https://doc.rust-lang.org/std/time/struct.Instant.html#method.now
[`time::Instant`]:https://doc.rust-lang.org/std/time/struct.Instant.html
