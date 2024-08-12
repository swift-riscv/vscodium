# VSCodium
*Packaging VSCodium for riscv64 - Ubuntu / Debian*

`VSCodium` for `riscv64` releases are available here [VSCodium](https://github.com/VSCodium/vscodium/releases) but there are no `.deb` install packages available.

We can create an `apt .deb` install package for `riscv64` by replacing `codium` in the `arm64` with the `riscv64` release.

This can be then repackaged into a fully `riscv64` compatable install `.deb` package.
