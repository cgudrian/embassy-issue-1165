# Embassy Build Failure with Cargo Workspaces

This is a minimal Embassy Project that fails to build within the context of a
Cargo Workspace but fine without it.

The failure is triggered by Rust trying to compile the crate `stm32-metapac` for
the host instead for the target platform. This does not happend if the build is
run without a workspace definition.

## Steps to reproduce

- Checkout this repository.
- Run `cargo build`.
- The build fails with this error message:
        
        Compiling stm32-metapac v0.1.0 (https://github.com/embassy-rs/embassy.git#825b6710)
        LLVM ERROR: Global variable '__INTERRUPTS' has an invalid section specifier '.vector_table.interrupts': mach-o section specifier requires a segment and section separated by a comma.

Note: The message might differ slightly depending on the operating system you're
using.

If the top-level `Cargo.toml` is renamed or removed (thus removing the
workspace), the build succeeds:
```shell
$ rm Cargo.toml
$ cd app
$ cargo build
```
