## 根据字母数字创建随机密码

[![rand-badge]][rand] [![cat-os-badge]][cat-os]

以下是用[`Alphanumeric`] 从 `A-Z,
a-z, 0-9`中随机生成给定长度的由随机 ASCII字符组成的字符串的例子。

```rust,ignore
extern crate rand;

use rand::{thread_rng, Rng};
use rand::distributions::Alphanumeric;

fn main() {
    let rand_string: String = thread_rng()
        .sample_iter(&Alphanumeric)
        .take(30)
        .collect();

    println!("{}", rand_string);
}
```

[`Alphanumeric`]: https://docs.rs/rand/*/rand/distributions/struct.Alphanumeric.html

