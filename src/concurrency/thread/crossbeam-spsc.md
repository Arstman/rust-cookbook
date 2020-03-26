# 在两个线程之间传递数据

[![crossbeam-badge]][crossbeam] [![cat-concurrency-badge]][cat-concurrency]

本示例使用 [crossbeam-channel] 设立一个单生产者（producer）单消费者（ consumer）即(SPSC)的通道。 使用[`crossbeam::scope`] 和 [`Scope::spawn`]  创建  [ex-crossbeam-spawn] 的实例来管理生产者线程。在两个线程之间使用一个[`crossbeam_channel::unbounded`]  通道交换数据，这意味着可存储消息的数量没有限制。生产者线程在两次消息之间睡眠半秒。

```rust
extern crate crossbeam;
extern crate crossbeam_channel;

use std::{thread, time};
use crossbeam_channel::unbounded;

fn main() {
    let (snd, rcv) = unbounded();
    let n_msgs = 5;
    crossbeam::scope(|s| {
        s.spawn(|_| {
            for i in 0..n_msgs {
                snd.send(i).unwrap();
                thread::sleep(time::Duration::from_millis(100));
            }
        });
    }).unwrap();
    for _ in 0..n_msgs {
        let msg = rcv.recv().unwrap();
        println!("Received {}", msg);
    }
}
```

[crossbeam-channel]: https://docs.rs/crate/crossbeam-channel/
[ex-crossbeam-spawn]: concurrency/threads.html#spawn-a-short-lived-thread
[`crossbeam::scope`]: https://docs.rs/crossbeam/*/crossbeam/fn.scope.html
[`Scope::spawn`]: https://docs.rs/crossbeam/*/crossbeam/thread/struct.Scope.html#method.spawn
[`crossbeam_channel::unbounded`]: https://docs.rs/crossbeam-channel/*/crossbeam_channel/fn.unbounded.html
