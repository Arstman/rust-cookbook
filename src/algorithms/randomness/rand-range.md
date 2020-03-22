## 生成一定范围内的随机数

[![rand-badge]][rand] [![cat-science-badge]][cat-science]

使用 [`Rng::gen_range`] 生成一个半开`[0, 10)`区间（不包括`10`）内的随机数

```rust,ignore
extern crate rand;

use rand::Rng;

fn main() {
    let mut rng = rand::thread_rng();
    println!("Integer: {}", rng.gen_range(0, 10));
    println!("Float: {}", rng.gen_range(0.0, 10.0));
}
```

使用[`Uniform`] 同样可以获得 [均匀分布]的随机值，其效果虽然一样，但在重复生成相同范围内的数字时可能会更快。

```rust,ignore
extern crate rand;


use rand::distributions::{Distribution, Uniform};

fn main() {
    let mut rng = rand::thread_rng();
    let die = Uniform::from(1..7);

    loop {
        let throw = die.sample(&mut rng);
        println!("Roll the die: {}", throw);
        if throw == 6 {
            break;
        }
    }
}
```

[`Uniform`]: https://docs.rs/rand/*/rand/distributions/uniform/struct.Uniform.html
[`Rng::gen_range`]: https://doc.rust-lang.org/rand/*/rand/trait.Rng.html#method.gen_range
[uniform distribution]: https://en.wikipedia.org/wiki/Uniform_distribution_(continuous)
