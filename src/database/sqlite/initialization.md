## 创建 SQLite 数据库

[![rusqlite-badge]][rusqlite] [![cat-database-badge]][cat-database]

使用 `rusqlite` 创建并打开 SQLite 数据库。有关在Windows上进行编译的信息，请参见 [crate][documentation] 的文档。

[`Connection::open`] 会打开数据库，如果数据库不存在将会创建一个。

```rust,no_run
extern crate rusqlite;

use rusqlite::{Connection, Result};
use rusqlite::NO_PARAMS;

fn main() -> Result<()> {
    let conn = Connection::open("cats.db")?;

    conn.execute(
        "create table if not exists cat_colors (
             id integer primary key,
             name text not null unique
         )",
        NO_PARAMS,
    )?;
    conn.execute(
        "create table if not exists cats (
             id integer primary key,
             name text not null,
             color_id integer not null references cat_colors(id)
         )",
        NO_PARAMS,
    )?;

    Ok(())
}
```

[`Connection::open`]: https://docs.rs/rusqlite/*/rusqlite/struct.Connection.html#method.open

[documentation]: https://github.com/jgallagher/rusqlite#user-content-notes-on-building-rusqlite-and-libsqlite3-sys
