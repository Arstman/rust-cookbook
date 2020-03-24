## 解析命令行参数

[![clap-badge]][clap] [![cat-command-line-badge]][cat-command-line]

这是使用`clap`的样式构建器构建一个命令行应用的界面的示例。clap的文档 [documentation] 还提供了另外两种实例化命令行应用的方式。

在构建器的样式中，使用`value_of`来获取由 `with_name` 定义的唯一参数标识符，用 `short` 和 `long` 选项来控制期望的用户输入风格： short 类似 `-f` ， long 类似 `--file` 。

```rust
extern crate clap;

use clap::{Arg, App};

fn main() {
    let matches = App::new("My Test Program")
        .version("0.1.0")
        .author("Hackerman Jones <hckrmnjones@hack.gov>")
        .about("Teaches argument parsing")
        .arg(Arg::with_name("file")
                 .short("f")
                 .long("file")
                 .takes_value(true)
                 .help("A cool file"))
        .arg(Arg::with_name("num")
                 .short("n")
                 .long("number")
                 .takes_value(true)
                 .help("Five less than your favorite number"))
        .get_matches();

    let myfile = matches.value_of("file").unwrap_or("input.txt");
    println!("The file passed is: {}", myfile);

    let num_str = matches.value_of("num");
    match num_str {
        None => println!("No idea what your favorite number is."),
        Some(s) => {
            match s.parse::<i32>() {
                Ok(n) => println!("Your favorite number must be {}.", n + 5),
                Err(_) => println!("That's not a number! {}", s),
            }
        }
    }
}
```

`clap` 会自动生成应用的使用帮助（Usage Information），本例生成的应用使用帮助如下：

```
My Test Program 0.1.0
Hackerman Jones <hckrmnjones@hack.gov>
Teaches argument parsing

USAGE:
    testing [OPTIONS]

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information

OPTIONS:
    -f, --file <file>     A cool file
    -n, --number <num>    Five less than your favorite number
```

我们可以通过运行如下命令来测试应用。

```
$ cargo run -- -f myfile.txt -n 251
```

输出结果为:

```
The file passed is: myfile.txt
Your favorite number must be 256.
```

[documentation]: https://docs.rs/clap/
