# 关于 "Cookin' with Rust"

## 目录

- [这本书是给谁的](#who-this-book-is-for)
- [如何阅读本书](#how-to-read-this-book)
- [如何使用书中的专题](#how-to-use-the-recipes)
- [有关错误处理的注意事项](#a-note-about-error-handling)
- [关于 crate 的说明](#a-note-about-crate-representation)

## 这本书是给谁的

本书适用于Rust新手程序员，以便他们可以快速了解Rust crate生态系统的功能。对于有经验的Rust程序员，他们也应该能在各个专题中找到如何完成常见任务的简单提示。



## 如何阅读本书

本书的 [index] 索引页包含了所有专题的完整列表， 分为几个部分: "基础", "编码", "并发", 等等.  这些部分本身内部会或多或少地按顺序排列，随后的部分则更高级，并且偶尔会基于前面部分的概念。

在索引中，每个章节部分都包含有一个专题列表，其中有关某个专题要达成之任务的简单说明，例如“生成一定范围内的随机数”；并且每个专题都有一个*徽标*标明其使用的*crate*，如 [![rand-badge]][rand], 并有标明其在 [crates.io] 上的分类, 例如
[![cat-science-badge]][cat-science].

对于Rust新手来说，按顺序从头至尾阅读是比较适合的，这样做应该能对crate生态系统有一个比较全面的了解。 可以点击在索引页中的章节部分，或者从侧边栏中点击，以导航到该部分进行阅读。

如果你只是在寻找某个简单任务解决方案，那么从导航里面寻找需要的专题可能有点难度。更简便的方式，是从索引页中查找你感兴趣的crate和类别，然后点击合适的专题去浏览， 不过后续将会针对这一点改进。



## 如何使用书中的专题

专题旨在让你查看可直接用在工作中的代码，每个专题都有详细的解释，并指导你如何获得更多信息。

Recipes are designed to give you instant access to working code, along
with a full explanation of what it is doing, and to guide you to
further information.

本书中的所有专题都是完整的、自包含的代码程序，因此你可以将它们直接复制到自己的项目中进行试验；为此，请按照以下说明进行操作。

考虑以下示例以“生成一个范围内的随机数”：

[![rand-badge]][rand] [![cat-science-badge]][cat-science]

```rust
extern crate rand;
use rand::Rng;

fn main() {
    let mut rng = rand::thread_rng();
    println!("Random f64: {}", rng.gen::<f64>());
}
```

要在本地使用它，我们可以运行以下命令来创建一个新的cargo项目，并切换到该目录：


```sh
cargo new my-example --bin
cd my-example
```

Now, we also need to add the necessary crates to [Cargo.toml], as
indicated by the crate badges, in this case just "rand". To do so,
we'll use the `cargo add` command, which is provided by the
[`cargo-edit`] crate, which we need to install first:

接着，我们需要将必要的crate添加到[Cargo.toml](http://doc.crates.io/manifest.html)，如专题的crate标志所示，在本例中为“ rand”。为此，我们将使用由[`cargo-edit`] crate 提供的`cargo add`命令，首先需要安装该命令 ：

```sh
cargo install cargo-edit
cargo add rand
```

现在，您可以把`src/main.rs`替换为示例的内容并运行它：:

```sh
cargo run
```

示例附带的crate徽章会链接到其在[docs.rs](https://docs.rs/)上的完整文档，如果你确定这个crate正是你需要的，那么该文档常常会是你下一步需要阅读的。



## 有关错误处理的注意事项

如果处理得当，Rust的错误处理通常都很可靠。不过在如今的Rust里错误处理都有不少的样板代码要写。因此，经常看到在Rush实例代码中充满了`unwrap` 调用，而不是采用适当的错误处理。

由于本书的专题旨在鼓励将它们原汁原味地用于最佳实践中去，因此在涉及`Result` 类型时会正确地设置错误处理。 

我们采用的基本模式是使用 `fn main() -> Result`。

该结构通常如下所示：

```rust
#[macro_use]
extern crate error_chain;

use std::net::IpAddr;
use std::str;

error_chain! {
    foreign_links {
        Utf8(std::str::Utf8Error);
        AddrParse(std::net::AddrParseError);
    }
}

fn main() -> Result<()> {
    let bytes = b"2001:db8::1";

    // Bytes to string.
    let s = str::from_utf8(bytes)?;

    // String to IP address.
    let addr: IpAddr = s.parse()?;

    println!("{:?}", addr);
    Ok(())
}

```

以上例子是使用 `error_chain!` 宏来自定义 `Error` 和
`Result` 类型, 以及来自标准库中两种错误类型的自动转换，自动转换使`?运算符能够被正确处理。

为了便于阅读，错误处理的样板代码默认情况下是隐藏的，如下所示。要阅读全部内容，请点击"expand" (<i class="fa fa-expand"></i>) 按钮（位于代码段的右上角）。

```rust
# #[macro_use]
# extern crate error_chain;
extern crate url;

use url::{Url, Position};
#
# error_chain! {
#     foreign_links {
#         UrlParse(url::ParseError);
#     }
# }

fn main() -> Result<()> {
    let parsed = Url::parse("https://httpbin.org/cookies/set?k2=v2&k1=v1")?;
    let cleaned: &str = &parsed[..Position::AfterPath];
    println!("cleaned: {}", cleaned);
    Ok(())
}
```

For more background on error handling in Rust, read [this page of the
Rust book][error-docs] and [this blog post][error-blog].

有关Rust中错误处理的更多背景知识，请阅读[Rust书的本页][error-docs]和[这篇文章][error-blog]。



## 关于 crate 的说明

本书的终极目标是旨在覆盖大部分的Rust crate生态系统，但自本项目开始启动到呈现至今，所涉及的范围依然有限。我们认为，（以慢打快）由一个小的范围开始慢慢地逐步扩展的方式，有助于保证本项目快速成长为高质量的资源项目，并随着项目内容增长而保持一致的质量水平。

目前，本cookbook主要关注标准库、核心库以及一些基础crate库——这些crate库构建了最常见的编程任务，而其余的crate则建立在这些基础crate库之上。

本项目与 [Rust Libz Blitz] 密切相关，[Rust Libz Blitz] 是用于审查和改进这些crate质量的项目，因此它在很大程度上影响了对crate的选择， 凡是已经进入评估程序的crate都属于本cookbook的选择范围，同时正待评估的crate也同样属于本书选择范围内。 

{{#include links.md}}

[index]: intro.html
[error-docs]: https://doc.rust-lang.org/book/error-handling.html
[error-blog]: https://brson.github.io/2016/11/30/starting-with-error-chain
[error-chain]: https://docs.rs/error-chain/
[Rust Libz Blitz]: https://internals.rust-lang.org/t/rust-libz-blitz/5184
[crates.io]: https://crates.io
[docs.rs]: https://docs.rs
[Cargo.toml]: http://doc.crates.io/manifest.html
[`cargo-edit`]: https://github.com/killercup/cargo-edit
