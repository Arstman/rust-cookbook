## 将错误信息记录到控制台

[![log-badge]][log] [![env_logger-badge]][env_logger] [![cat-debugging-badge]][cat-debugging]

正确的错误处理将异常视为例外。  这里介绍一个将错误记录到 stderr 的`log` 宏[`error!`]。

```rust
#[macro_use]
extern crate log;
extern crate env_logger;

fn execute_query(_query: &str) -> Result<(), &'static str> {
    Err("I'm afraid I can't do that")
}

fn main() {
    env_logger::init();

    let response = execute_query("DROP TABLE students");
    if let Err(err) = response {
        error!("Failed to execute query: {}", err);
    }
}
```

[`error!`]: https://docs.rs/log/*/log/macro.error.html
