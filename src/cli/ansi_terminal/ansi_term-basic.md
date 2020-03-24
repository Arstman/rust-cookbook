## ANSI 终端

[![ansi_term-badge]][ansi_term] [![cat-command-line-badge]][cat-command-line]

此程序描述了 [`ansi_term` crate] 的用法，以及如何将其应用于控制ANSI 终端上的颜色和格式，例如蓝色粗体文本或黄色带下划线的文本，

[`ansi_term` crate] 中有两个主要数据结构：[`ANSIString`] 和 [`Style`] 。  [`Style`] 控制样式信息：颜色，文本是粗体，闪烁还是其他， Colour 变量可以简单地用于设置前景颜色样式； [`ANSIString`] 是与 [`Style`] 配对的字符串。

注意：英式英语中使用“ ***Colour***”*而不是“ ***Color***”*，不要弄错了。



### 将彩色文本打印到终端

```rust
extern crate ansi_term;

use ansi_term::Colour;

fn main() {
    println!("This is {} in color, {} in color and {} in color",
             Colour::Red.paint("red"),
             Colour::Blue.paint("blue"),
             Colour::Green.paint("green"));
}
```

### 终端中的粗体

对于任何比设置普通前景色更复杂的事情，都需要构造 `Style`结构，用 [`Style::new()`] 可以创建此结构并用链式调用来更改属性项。

```rust
extern crate ansi_term;

use ansi_term::Style;

fn main() {
    println!("{} and this is not",
             Style::new().bold().paint("This is Bold"));
}
```
### 终端中的粗体和彩色文本

`Colour` 实现了很多与 `Style` 相似的方法，同样可以链式调用。

```rust
extern crate ansi_term;

use ansi_term::Colour;
use ansi_term::Style;

fn main(){
    println!("{}, {} and {}",
             Colour::Yellow.paint("This is colored"),
             Style::new().bold().paint("this is bold"),
             Colour::Yellow.bold().paint("this is bold and colored"));
}
```

[documentation]: https://docs.rs/ansi_term/
[`ansi_term` crate]: https://crates.io/crates/ansi_term
[`ANSIString`]: https://docs.rs/ansi_term/*/ansi_term/type.ANSIString.html
[`Style`]: https://docs.rs/ansi_term/*/ansi_term/struct.Style.html
[`Style::new()`]: https://docs.rs/ansi_term/0.11.0/ansi_term/struct.Style.html#method.new
