# 开发工具

{{#include development_tools/debugging.md}}

## 版本控制

| Recipe | Crates | Categories |
|--------|--------|------------|
| [解析版本字符串并递增版本号][ex-semver-increment] | [![semver-badge]][semver] | [![cat-config-badge]][cat-config] |
| [解析复杂的版本字符串][ex-semver-complex] | [![semver-badge]][semver] | [![cat-config-badge]][cat-config] |
| [判断给定版本是否为预发布][ex-semver-prerelease] | [![semver-badge]][semver] | [![cat-config-badge]][cat-config] |
| [查找满足给范围中最新版本][ex-semver-latest] | [![semver-badge]][semver] | [![cat-config-badge]][cat-config] |
| [检查外部命令版本的兼容性][ex-semver-command] | [![semver-badge]][semver] | [![cat-text-processing-badge]][cat-text-processing] [![cat-os-badge]][cat-os]

## 编译时

| Recipe | Crates | Categories |
|--------|--------|------------|
| [静态编译并链接到已封装的C库][ex-cc-static-bundled] | [![cc-badge]][cc] | [![cat-development-tools-badge]][cat-development-tools] |
| [静态编译并链接到已封装的C++库][ex-cc-static-bundled-cpp] | [![cc-badge]][cc] | [![cat-development-tools-badge]][cat-development-tools] |
| [设置自定义编译C库][ex-cc-custom-defines] | [![cc-badge]][cc] | [![cat-development-tools-badge]][cat-development-tools] |

[ex-semver-increment]: development_tools/versioning.html#parse-and-increment-a-version-string
[ex-semver-complex]: development_tools/versioning.html#parse-a-complex-version-string
[ex-semver-prerelease]: development_tools/versioning.html#check-if-given-version-is-pre-release
[ex-semver-latest]: development_tools/versioning.html#find-the-latest-version-satisfying-given-range
[ex-semver-command]: development_tools/versioning.html#check-external-command-version-for-compatibility

[ex-cc-static-bundled]: development_tools/build_tools.html#compile-and-link-statically-to-a-bundled-c-library
[ex-cc-static-bundled-cpp]: development_tools/build_tools.html#compile-and-link-statically-to-a-bundled-c-library-1
[ex-cc-custom-defines]: development_tools/build_tools.html#compile-a-c-library-while-setting-custom-defines

{{#include links.md}}
