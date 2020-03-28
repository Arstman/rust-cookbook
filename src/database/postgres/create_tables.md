## 在 Postgres 数据库中创建表

[![postgres-badge]][postgres] [![cat-database-badge]][cat-database]

使用 [`postgres`] crate 在Postgres数据库中创建表。

借助 [`Connection::connect`] 连接到已有的数据库。 本例使用带有的URL字符串格式来连接， 假设现有名为 `library` 的数据库， 用户名为 `postgres` 密码为 `postgres`。

```rust,no_run
extern crate postgres;

use postgres::{Connection, TlsMode, Error};

fn main() -> Result<(), Error> {
    let conn = Connection::connect("postgresql://postgres:postgres@localhost/library", 
                                    TlsMode::None)?;
    
     conn.execute("CREATE TABLE IF NOT EXISTS author (
                    id              SERIAL PRIMARY KEY,
                    name            VARCHAR NOT NULL,
                    country         VARCHAR NOT NULL
                  )", &[])?;

    conn.execute("CREATE TABLE IF NOT EXISTS book  (
                    id              SERIAL PRIMARY KEY,
                    title           VARCHAR NOT NULL,
                    author_id       INTEGER NOT NULL REFERENCES author
                )", &[])?;

    Ok(())

}
```

[`postgres`]: https://docs.rs/postgres/0.15.2/postgres/
[`Connection::connect`]: https://docs.rs/postgres/0.15.2/postgres/struct.Connection.html#method.connect
