## 生成随机数

[![rand-badge]][rand] [![cat-science-badge]][cat-science]

利用随机数生成器[`rand::Rng`] 通过 [`rand::thread_rng`]来帮助生成随机数.  每个线程都会单独初始化生成器； 生成的随机整数会在类型范围内均匀分布 （译注：例如u8类型，结果整数会在0-255范围内），浮点数则从0 至1均匀分布，但不包括1。

```rust
extern crate rand;

use rand::Rng;

fn main() {
    let mut rng = rand::thread_rng();

    let n1: u8 = rng.gen();
    let n2: u16 = rng.gen();
    println!("Random u8: {}", n1);
    println!("Random u16: {}", n2);
    println!("Random u32: {}", rng.gen::<u32>());
    println!("Random i32: {}", rng.gen::<i32>());
    println!("Random float: {}", rng.gen::<f64>());
}
```

[`rand::Rng`]: https://docs.rs/rand/*/rand/trait.Rng.html
[`rand::thread_rng`]: https://docs.rs/rand/*/rand/fn.thread_rng.html

