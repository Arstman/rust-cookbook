## 结构体类型Vec排序

[![std-badge]][std] [![cat-science-badge]][cat-science]

以下示例对含有 `name` 和 `age` 两个属性字段的结构体 Person进行自然排序（按name 和 age属性字段）。要让Person结构体可排序，需要有4个trait： [`Eq`]，[`PartialEq`]， [`Ord`] 和 [`PartialOrd`]。 这些trait只需简单地派生（derived）即可。另外还可以通过提供一个自定义的比较函数给到[`vec:sort_by`] 方法，来仅按age排序。

```rust
#[derive(Debug, Eq, Ord, PartialEq, PartialOrd)]
struct Person {
    name: String,
    age: u32
}

impl Person {
    pub fn new(name: String, age: u32) -> Self {
        Person {
            name,
            age
        }
    }
}

fn main() {
    let mut people = vec![
        Person::new("Zoe".to_string(), 25),
        Person::new("Al".to_string(), 60),
        Person::new("John".to_string(), 1),
    ];

    // Sort people by derived natural order (Name and age)
    people.sort();

    assert_eq!(
        people,
        vec![
            Person::new("Al".to_string(), 60),
            Person::new("John".to_string(), 1),
            Person::new("Zoe".to_string(), 25),
        ]);

    // Sort people by age
    people.sort_by(|a, b| b.age.cmp(&a.age));

    assert_eq!(
        people,
        vec![
            Person::new("Al".to_string(), 60),
            Person::new("Zoe".to_string(), 25),
            Person::new("John".to_string(), 1),
        ]);

}

```

[`Eq`]: https://doc.rust-lang.org/std/cmp/trait.Eq.html
[`PartialEq`]: https://doc.rust-lang.org/std/cmp/trait.PartialEq.html
[`Ord`]: https://doc.rust-lang.org/std/cmp/trait.Ord.html
[`PartialOrd`]: https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html
[`vec:sort_by`]: https://doc.rust-lang.org/std/vec/struct.Vec.html#method.sort_by
