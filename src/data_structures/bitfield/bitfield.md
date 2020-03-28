## 定义表示为位域（bitfield）的类型并对其操作

[![bitflags-badge]][bitflags] [![cat-no-std-badge]][cat-no-std]

借助 [`bitflags!`] 宏来创建类型安全的位域（bitfield）类型 `MyFlags`，并实现基本的 `clear` 操作及 [`Display`] trait。接着展示了如何对其进行基本的按位运算和格式化。

```rust
#[macro_use]
extern crate bitflags;

use std::fmt;

bitflags! {
    struct MyFlags: u32 {
        const FLAG_A       = 0b00000001;
        const FLAG_B       = 0b00000010;
        const FLAG_C       = 0b00000100;
        const FLAG_ABC     = Self::FLAG_A.bits
                           | Self::FLAG_B.bits
                           | Self::FLAG_C.bits;
    }
}

impl MyFlags {
    pub fn clear(&mut self) -> &mut MyFlags {
        self.bits = 0;  
        self
    }
}

impl fmt::Display for MyFlags {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "{:032b}", self.bits)
    }
}

fn main() {
    let e1 = MyFlags::FLAG_A | MyFlags::FLAG_C;
    let e2 = MyFlags::FLAG_B | MyFlags::FLAG_C;
    assert_eq!((e1 | e2), MyFlags::FLAG_ABC);   
    assert_eq!((e1 & e2), MyFlags::FLAG_C);    
    assert_eq!((e1 - e2), MyFlags::FLAG_A);    
    assert_eq!(!e2, MyFlags::FLAG_A);           

    let mut flags = MyFlags::FLAG_ABC;
    assert_eq!(format!("{}", flags), "00000000000000000000000000000111");
    assert_eq!(format!("{}", flags.clear()), "00000000000000000000000000000000");
    assert_eq!(format!("{:?}", MyFlags::FLAG_B), "FLAG_B");
    assert_eq!(format!("{:?}", MyFlags::FLAG_A | MyFlags::FLAG_B), "FLAG_A | FLAG_B");
}
```

[`bitflags!`]: https://docs.rs/bitflags/*/bitflags/macro.bitflags.html
[`Display`]: https://doc.rust-lang.org/std/fmt/trait.Display.html
