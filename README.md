# VSCodium
*Packaging VSCodium for riscv64 - Ubuntu / Debian*

`VSCodium` for `riscv64` releases are available from [VSCodium](https://github.com/VSCodium/vscodium/releases) but there are no `.deb` install packages available.

We can create an `apt .deb` install package for `riscv64` by replacing `codium` in the `arm64` package with the `riscv64` release.

This can then be repackaged into a fully `riscv64` compatable apt install `.deb` package.

The `.deb` packages are created using `fpm` - https://github.com/jordansissel/fpm and built on our [Milk-V Pioneer](https://milkv.io/pioneer) `riscv64` build server.

</br>

[![Build Status](https://ci.swiftlang.xyz/view/riscv64/job/vscodium-riscv64-deb/badge/icon)](https://ci.swiftlang.xyz/view/riscv64/job/vscodium-riscv64-deb/)
