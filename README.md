![Test](https://github.com/Peco602/rust-universal-compiler/actions/workflows/test.yml/badge.svg)
[![Mentioned in awesome-docker](https://awesome.re/mentioned-badge.svg)](https://github.com/veggiemonk/awesome-docker)

# Rust Universal Compiler Docker image

Container solution to compile Rust projects for Linux, macOS and Windows.


## Build the image

```ps1
docker build -t rust-universal-compiler:latest .
```

## Configure the project

To allow cross-compilation from Linux to Windows and MacOS, it is necessary to create in the project folder the `.cargo/config.toml` file containing the following lines:

```ini
[target.x86_64-pc-windows-msvc]
rustflags = ["-C", "target-feature=+crt-static"]

[target.aarch64-apple-darwin]
linker = "aarch64-apple-darwin20.4-clang"
ar = "aarch64-apple-darwin-ar"
```

## Compile the project

Compile for Linux (`x86_64-unknown-linux-gnu`):

```bash
docker run --rm -v $PWD/test-project:/app -w /app rust-universal-compiler:latest cargo build --target x86_64-unknown-linux-gnu --release
```

Compile for MacOS (`aarch64-apple-darwin`):

```bash
docker run --rm -v $PWD/test-project:/app -w /app rust-universal-compiler:latest cargo build --target aarch64-apple-darwin --release
```

Compile for Windows (`x86_64-pc-windows-msvc`):

```bash
docker run --rm -v $PWD/test-project:/app -w /app rust-universal-compiler:latest cargo build --target x86_64-pc-windows-msvc --release
```

## DockerHub

- [peco602/rust-universal-compiler](https://hub.docker.com/r/peco602/rust-universal-compiler)


## Bibliography

- https://github.com/Jake-Shadle/xwin
- https://wapl.es/rust/2019/02/17/rust-cross-compile-linux-to-macos.html
