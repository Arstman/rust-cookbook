## 创建短期线程

[![crossbeam-badge]][crossbeam] [![cat-concurrency-badge]][cat-concurrency]

本示例使用 [crossbeam] crate, 该库提供了用于并发和并行编程的数据结构和方法函数。 [`Scope::spawn`] 创建一个新的作用域线程，并确保在传给 [`crossbeam::scope`] 的闭包返回之前终止，这意味着可以从（作用域外层的）调用者函数中引用数据。

本示例将数组分成两部分，并在单独的线程中执行操作。

```rust
extern crate crossbeam;

fn main() {
    let arr = &[1, 25, -4, 10];
    let max = find_max(arr);
    assert_eq!(max, Some(25));
}

fn find_max(arr: &[i32]) -> Option<i32> {
    const THRESHOLD: usize = 2;
  
    if arr.len() <= THRESHOLD {
        return arr.iter().cloned().max();
    }

    let mid = arr.len() / 2;
    let (left, right) = arr.split_at(mid);
  
    crossbeam::scope(|s| {
        let thread_l = s.spawn(|_| find_max(left));
        let thread_r = s.spawn(|_| find_max(right));
  
        let max_l = thread_l.join().unwrap()?;
        let max_r = thread_r.join().unwrap()?;
  
        Some(max_l.max(max_r))
    }).unwrap()
}
```

[`crossbeam::scope`]: https://docs.rs/crossbeam/*/crossbeam/fn.scope.html
[`Scope::spawn`]: https://docs.rs/crossbeam/*/crossbeam/thread/struct.Scope.html#method.spawn
