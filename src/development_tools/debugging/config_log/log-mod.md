## 为每个模块启用日志级别

[![log-badge]][log] [![env_logger-badge]][env_logger] [![cat-debugging-badge]][cat-debugging]

创建两个嵌套模块`foo` 和`foo::bar` , 为它们设置单独的[`RUST_LOG`] 日志环境变量. 

```rust
#[macro_use]
extern crate log;
extern crate env_logger;

mod foo {
    mod bar {
        pub fn run() {
            warn!("[bar] warn");
            info!("[bar] info");
            debug!("[bar] debug");
        }
    }

    pub fn run() {
        warn!("[foo] warn");
        info!("[foo] info");
        debug!("[foo] debug");
        bar::run();
    }
}

fn main() {
    env_logger::init();
    warn!("[root] warn");
    info!("[root] info");
    debug!("[root] debug");
    foo::run();
}
```

[`RUST_LOG`] 环境变量控制着 [`env_logger`][env_logger] 输出. 
如以下运行 `test`程序的命令所示, 每个模块的变量声明是形如 `path::to::module=log_level`的条目, 用逗号分隔 :

```bash
RUST_LOG="warn,test::foo=info,test::foo::bar=debug" ./test
```

本例子将 [`log::Level`] 设置为 `warn`, 模块 `foo` 和模块 `foo::bar` 则分别设置为 `info` 和 `debug`.

```bash
WARN:test: [root] warn
WARN:test::foo: [foo] warn
INFO:test::foo: [foo] info
WARN:test::foo::bar: [bar] warn
INFO:test::foo::bar: [bar] info
DEBUG:test::foo::bar: [bar] debug
```

[`log::Level`]: https://docs.rs/log/*/log/enum.Level.html
[`RUST_LOG`]: https://docs.rs/env_logger/*/env_logger/#enabling-logging
