## 将文件夹压缩至tarball

[![flate2-badge]][flate2] [![tar-badge]][tar] [![cat-compression-badge]][cat-compression]

将 `/var/log` 目录文件夹压缩至 `archive.tar.gz`.

创建一个文件 [`File`] ，并用 [`GzEncoder`] 和 [`tar::Builder`]包裹起来。 </br>Adds contents of `/var/log` directory recursively into the archive
under `backup/logs`path 使用 [`Builder::append_dir_all`] 将`/var/log` 目录文件夹下的文件递归地添加到位于`backup/logs` 路径下的压缩包文件中，[`GzEncoder`] 负责在数据实际写入`archive.tar.gz`之前压缩数据。

```rust,no_run
extern crate tar;
extern crate flate2;

use std::fs::File;
use flate2::Compression;
use flate2::write::GzEncoder;

fn main() -> Result<(), std::io::Error> {
    let tar_gz = File::create("archive.tar.gz")?;
    let enc = GzEncoder::new(tar_gz, Compression::default());
    let mut tar = tar::Builder::new(enc);
    tar.append_dir_all("backup/logs", "/var/log")?;
    Ok(())
}
```

[`Builder::append_dir_all`]: https://docs.rs/tar/*/tar/struct.Builder.html#method.append_dir_all
[`File`]: https://doc.rust-lang.org/std/fs/struct.File.html
[`GzEncoder`]: https://docs.rs/flate2/*/flate2/write/struct.GzEncoder.html
[`tar::Builder`]: https://docs.rs/tar/*/tar/struct.Builder.html
