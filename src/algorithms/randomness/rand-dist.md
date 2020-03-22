## 生成给定分布的随机数

[![rand-badge]][rand] [![cat-science-badge]][cat-science]

默认情况下，生成的随机数呈 [均匀分布] （译注：也叫”连续均匀分布“）.
要生成其他分布模型的随机数，请先实例化一个分布, 然后借助随机数生成器 [`rand::Rng`]，利用
[`Distribution::sample`] 从该分布中采样。


 [可选的分布模型在列于此][rand-distributions]. 以下是一个使用[`Normal正态分布`]的例子.

```
extern crate rand;

use rand::distributions::{Normal, Distribution};

fn main() {
  let mut rng = rand::thread_rng();
  let normal = Normal::new(2.0, 3.0);
  let v = normal.sample(&mut rng);
  println!("{} is from a N(2, 9) distribution", v)
}
```

[`Distribution::sample`]: https://docs.rs/rand/*/rand/distributions/trait.Distribution.html#tymethod.sample
[`Normal`]: https://docs.rs/rand/*/rand/distributions/normal/struct.Normal.html
[`rand::Rng`]: https://docs.rs/rand/*/rand/trait.Rng.html
[rand-distributions]: https://docs.rs/rand/*/rand/distributions/index.html

[uniform distribution]: https://en.wikipedia.org/wiki/Uniform_distribution_(continuous)
