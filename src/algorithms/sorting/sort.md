## Sort a Vector of Integers

[![std-badge]][std] [![cat-science-badge]][cat-science]

本示例通过[`vec::sort`] 方法对元素为整数类型的Vector 数组进行排序。也可以选择用 [`vec::sort_unstable`] ，该方法更快，但相等元素在排序之前的原始顺序不会被保留。（译注：即**不稳定排序**）

```rust
fn main() {
    let mut vec = vec![1, 5, 10, 2, 15];
    
    vec.sort();

    assert_eq!(vec, vec![1, 2, 5, 10, 15]);
}
```

[`vec::sort`]: https://doc.rust-lang.org/std/vec/struct.Vec.html#method.sort
[`vec::sort_unstable`]: https://doc.rust-lang.org/std/vec/struct.Vec.html#method.sort_unstable
