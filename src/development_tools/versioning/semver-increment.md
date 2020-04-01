## 解析版本字符串并递增版本号

[![semver-badge]][semver] [![cat-config-badge]][cat-config]

使用 [`Version::parse`] 从一个字面量字符串构造一个[`semver::Version`], 然后依递增主版本号.次版本号.修订号。

请注意，根据[语义化版本规范], 递增次要版本号会将补丁版本号重置为0，而递增主要版本号则会将次要版本号和补丁版本号都重置为0。

```rust
extern crate semver;

use semver::{Version, SemVerError};

fn main() -> Result<(), SemVerError> {
    let mut parsed_version = Version::parse("0.2.6")?;

    assert_eq!(
        parsed_version,
        Version {
            major: 0,
            minor: 2,
            patch: 6,
            pre: vec![],
            build: vec![],
        }
    );

    parsed_version.increment_patch();
    assert_eq!(parsed_version.to_string(), "0.2.7");
    println!("New patch release: v{}", parsed_version);

    parsed_version.increment_minor();
    assert_eq!(parsed_version.to_string(), "0.3.0");
    println!("New minor release: v{}", parsed_version);

    parsed_version.increment_major();
    assert_eq!(parsed_version.to_string(), "1.0.0");
    println!("New major release: v{}", parsed_version);

    Ok(())
}
```

[`semver::Version`]: https://docs.rs/semver/*/semver/struct.Version.html
[`Version::parse`]: https://docs.rs/semver/*/semver/struct.Version.html#method.parse

[语义化版本规范]: http://semver.org/
