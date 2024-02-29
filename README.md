# aya-t1

## Prerequisites

1. Install bpf-linker: `cargo install bpf-linker`

## Build eBPF

```bash
cargo xtask build-ebpf
```

To perform a release build you can use the `--release` flag.
You may also change the target architecture with the `--target` flag.

## Build Userspace

```bash
cargo build
```

## Run

```bash
## defult log_level=info
cargo xtask run
## debug日志
RUST_LOG=debug cargo xtask run
```
## 一些说明

使用`cargo generate https://github.com/aya-rs/aya-template`时，命名项目名称为`aya-t1`
共生成的项目代码目录三个：
- aya-t1：userspace代码
- aya-t1-common: userspace和内核空间ebpf代码共用的一些逻辑或变量
- aya-t1-ebpf：ebpf程序的实现，这里是使用rust实现的，ebpf-go则是由C实现的
（为什么ebpf程序在ebpf-go没有使用go实现呢，因为ebpf程序在加载到内核之前，需要编译为ebpf字节码，
c和rust能够通过llvm编译器生成这种字节码，而go语言的编译器不支持，另外还是运行时及内存管理的问题，
go的运行时相对庞大，且内存管理机制不适用于ebpf程序）