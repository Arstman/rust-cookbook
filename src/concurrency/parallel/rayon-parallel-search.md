## 使用给定谓词并行搜索项目

[![rayon-badge]][rayon] [![cat-concurrency-badge]][cat-concurrency]

本示例使用 [`rayon::find_any`] 和 [`par_iter`] 并行搜索 vector 以找到符合闭包中给定谓词的元素。

如果有多个元素满足[`rayon::find_any`]的闭包参数中定义的谓词If there are multiple elements satisfying the predicate 那么  `rayon` 返回第一个被找到的元素，不一定是第一个（顺序位置）元素。

请注意，闭包的参数是对引用的引用 (`&&x`) ，更多详情请参见有关 [`std::find`] 的讨论。

```rust
extern crate rayon;

use rayon::prelude::*;

fn main() {
    let v = vec![6, 2, 1, 9, 3, 8, 11];

    let f1 = v.par_iter().find_any(|&&x| x == 9);
    let f2 = v.par_iter().find_any(|&&x| x % 2 == 0 && x > 6);
    let f3 = v.par_iter().find_any(|&&x| x > 8);

    assert_eq!(f1, Some(&9));
    assert_eq!(f2, Some(&8));
    assert!(f3 > Some(&8));
}
```

[`par_iter`]: https://docs.rs/rayon/*/rayon/iter/trait.IntoParallelRefIterator.html#tymethod.par_iter
[`rayon::find_any`]: https://docs.rs/rayon/*/rayon/iter/trait.ParallelIterator.html#method.find_any
[`std::find`]: https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.find
