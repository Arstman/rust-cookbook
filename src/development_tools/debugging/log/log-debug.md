## 将调试消息记录到控制台

[![log-badge]][log] [![env_logger-badge]][env_logger] [![cat-debugging-badge]][cat-debugging]

`log` crate 提供了记录日志的工具， `env_logger` crate 则通过环境变量来配置日志生成。 [`debug!`] 宏用作格式化字符串,与标准库中的[`std::fmt`] 类似。

```rust
#[macro_use]
extern crate log;
extern crate env_logger;

fn execute_query(query: &str) {
    debug!("Executing query: {}", query);
}

fn main() {
    env_logger::init();

    execute_query("DROP TABLE students");
}
```

运行此代码时不会有任何输出，默认情况下日志级别error， 任何较低级别的都将被删除。
设置 `RUST_LOG` 环境变量以打印消息:

```
$ RUST_LOG=debug cargo run
```

这样Cargo会打印调试信息，然后在输出的最后一行显示以下行：

```
DEBUG:main: Executing query: DROP TABLE students
```

[`debug!`]: https://docs.rs/log/*/log/macro.debug.html
[`std::fmt`]: https://doc.rust-lang.org/std/fmt/
