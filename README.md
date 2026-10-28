# Omarchy-kernel-Debian-Ubuntu-aarch64

![Xanmod MAIN](https://github.com/Locietta/xanmod-kernel-WSL2/actions/workflows/MAIN.yml/badge.svg?branch=main)
![Xanmod LTS](https://github.com/Locietta/xanmod-kernel-WSL2/actions/workflows/LTS.yml/badge.svg?branch=main)
![](https://img.shields.io/github/license/wsl2-kernels/omarchy-kernel-debian-ubuntu-aarch64)
![version](https://img.shields.io/github/v/release/wsl2-kernels/omarchy-kernel-debian-ubuntu-aarch64)

An **unofficial** Omarchy kernel port for **Debian/Ubuntu aarch64**, featuring:

- **Omarchy's kernel** patches for GPU support
- **Compiled with Clang + ThinLTO** for additional optimizations
- **Automated builds** via GitHub Actions (always up-to-date)
- **Built For aarch64** architecture

## Usage

### Install via apt (Recommended)

#### Installation

```bash
# Add the repository
sudo apt install ./*.deb

# Restart WSL2 to apply
sudo reboot now
```

**That's it!** the kernel is installed

```bash
# other MAIN builds
# scoop install xanmod-WSL2-{x64v2, x64v3, skylake, zen3}
# scoop install xanmod-WSL2-addons-{x64v2, x64v3, skylake, zen3}

# LTS builds
# scoop install xanmod-WSL2-lts # alias to xanmod-WSL2-lts-x64v3
# scoop install xanmod-WSL2-lts-addons
# scoop install xanmod-WSL2-lts-{x64v2, x64v3, skylake, zen3}
# scoop install xanmod-WSL2-addons-lts-{x64v2, x64v3, skylake, zen3}
```

</details>

#### Update kernel

Run `scoop update *` to update all scoop installed apps including this kernel.

We recommend to run `scoop update *` instead of `scoop update xanmod-WSL2` alone to make sure the addons package is also updated and in sync with the kernel.

> **NOTE:** To make the kernel update applied, you have to reboot WSL2 after running scoop update!

### Manual Installation

It's also straightforward to manually install this kernel. For each arch, we release two files: the kernel image `bzImage` and an optional addon archive `bzImage-addons.vhdx.7z` that contains the VHDX with extra modules, headers and documentation.

The manual installation steps are as follows:

- Download kernel image from [releases](https://github.com/Locietta/xanmod-kernel-WSL2/releases)
  - optionally, download the addon archive if you need extra modules/headers/docs, then extract the `.vhdx` file from it
- Place it to somewhere appropriate. (e.g. `D:\.WSL\bzImage`)
- Edit and save the `%UserProfile%\.wslconfig` with following content:

```ini
[wsl2]
kernel = the\\path\\to\\bzImage
kernelModules = the\\path\\to\\bzImage-addons.vhdx ; optional
; e.g.
; kernel = D:\\.WSL\\bzImage
; kernelModules = D:\\.WSL\\bzImage-addons.vhdx
;
; Note that all `\` should be escaped with `\\`.
```

- Reboot your WSL2 to check your new kernel and enjoy!

When the addon VHDX is configured, WSL exposes the packaged artifacts below
`/lib/modules/$(uname -r)`:

- `build/` is the prepared kbuild tree for compiling external kernel modules.
- `build/usr/include/` contains the sanitized userspace API headers exported by
  `make headers_install`.
- `build/Documentation/` contains the documentation from the matching kernel
  sources.

## Troubleshooting

### Changes not applied after installation or update?

You must fully shut down WSL2 utill no WSL2 instances are running, then start it again to apply the new kernel.

```powershell
wsl --shutdown
wsl --list --running  # Should show "no running distributions"
```

### Modules are not loaded to `/lib/modules`?

Modules VHDX support is only available with WSL version **2.5.1** or later. Try running `wsl --version` to check your WSL version and use `wsl --update` to update WSL if needed.

### Can't find `.wslconfig` file?

It doesn't exist by default. Just create it manually in your user profile folder (e.g. `C:\Users\YourName\.wslconfig`).

> For more information about `.wslconfig`, see microsoft's official [documentation](https://docs.microsoft.com/en-us/windows/wsl/wsl-config#configure-global-options-with-wslconfig).

### Which architecture should I choose?

If you are unsure whether to use x64v2 or x64v3, you can visit [xanmod.org](https://xanmod.org/). There's literally a table showing all the CPU models and their corresponding x86_64 psABI levels.

You can also get a [checking script](https://dl.xanmod.org/check_x86-64_psabi.sh) from there.

## Development

🚧WIP

## Credits

- Linux community for the awesome OS kernel.
- Microsoft for WSL2 and dxgkrnl patches.
- XanMod project for various optimizations.
- LLVM/Clang for the compiler infrastructure.

## Contributing

We welcome contributions! You can:

- 🐛 Report bugs by opening an [issue](https://github.com/Locietta/xanmod-kernel-WSL2/issues/new?template=bug_report.yml)
- 💡 Suggest features via [issues](https://github.com/Locietta/xanmod-kernel-WSL2/issues/new?template=feature-request.yml)
- 🔧 Submit improvements through [pull requests](https://github.com/Locietta/xanmod-kernel-WSL2/pulls)
