## 解压缩tarball格式

[![flate2-badge]][flate2] [![tar-badge]][tar] [![cat-compression-badge]][cat-compression]



将位于当前工作目录中名为`archive.tar.gz`的tarball压缩包解压缩 ([`GzDecoder`]) 并提取 ([`Archive::unpack`]) 所有文件。

```rust,no_run
extern crate flate2;
extern crate tar;

use std::fs::File;
use flate2::read::GzDecoder;
use tar::Archive;

fn main() -> Result<(), std::io::Error> {
    let path = "archive.tar.gz";

    let tar_gz = File::open(path)?;
    let tar = GzDecoder::new(tar_gz);
    let mut archive = Archive::new(tar);
    archive.unpack(".")?;

    Ok(())
}
```

[`Archive::unpack`]: https://docs.rs/tar/*/tar/struct.Archive.html#method.unpack
[`GzDecoder`]: https://docs.rs/flate2/*/flate2/read/struct.GzDecoder.html

