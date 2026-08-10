<h3 align="center">
  <a href="#"><img src="https://raw.githubusercontent.com/armbian/.github/master/profile/logosmall.png" alt="Armbian logo"></a>
  <br><br>
</h3>

# Armbian Build Framework

The **Armbian Linux Build Framework** creates customizable OS images based on **Debian** or **Ubuntu** for **single-board computers (SBCs)** and embedded devices. It builds a complete Linux system — kernel, bootloader, and root filesystem — giving you control over versions, configuration, firmware, device trees, and system optimizations.

> **Looking for prebuilt images?** Use [Armbian Imager](https://github.com/armbian/imager/releases) — the easiest way to download and flash Armbian to your SD card or USB drive. Available for Linux, macOS, and Windows.

## Quick Start

```bash
git clone https://github.com/armbian/build
cd build
./compile.sh
```

<a href="#quick-start"><img src=".github/README.gif" alt="Build demonstration" width="100%"></a>

The framework supports **native**, **cross**, and **containerized** builds for multiple architectures (`x86_64`, `aarch64`, `armhf`, `riscv64`) and is suitable for development, testing, production, or automation.

## Build Host Requirements

### Hardware
- **RAM:** ≥8 GB (less with `KERNEL_BTF=no`)
- **Disk:** ~50 GB free space
- **Architecture:** x86_64, aarch64, or riscv64

### Operating System
- **Native builds:** Armbian or Ubuntu 24.04 (Noble)
- **Containerized:** any Docker-capable Linux
- **Windows:** WSL2 with Armbian/Ubuntu 24.04

### Software
- Superuser privileges (`sudo` or root)
- Up-to-date system (outdated Docker or other tools can cause failures)

## Repository Layout

| Path | Contents |
|:--|:--|
| `compile.sh` | Main entry point; sources `lib/single.sh` and dispatches to the CLI |
| `lib/` | Build framework libraries (Bash) |
| `config/boards/` | Per-board configuration files (`*.conf`, `*.csc`, `*.wip`, `*.eos`, `*.tvb`) |
| `config/bootenv/`, `config/bootscripts/` | U-Boot boot environment and boot script sources |
| `config/cli/`, `config/distributions/`, `config/sources/` | CLI/server package lists, per-release settings, and family/source definitions |
| `patch/` | Kernel, U-Boot and misc. patches, plus per-branch overlay Makefiles |
| `packages/` | Debian packaging bits (`armbian` kernel packaging, `bsp`, `bsp-cli`, `bsp-desktop`, `blobs`, `extras-buildpkgs`) |
| `extensions/` | Optional build extensions loadable via `ENABLE_EXTENSIONS=` |
| `tools/` | Developer helpers (e.g. `mk_format_patch`, `unifying_configs`) |
| `.github/` | Issue/PR templates, CODEOWNERS, labels, workflows |
| `action.yml` | Composite GitHub Action ("Rebuild Armbian") that wraps the build for reuse in workflows |
| `VERSION` | Framework version marker |

### Board support tiers

Board configs are named by file extension to signal their support status (see `config/distributions/README.md` and `config/boards/README.md`):

| Extension | Meaning |
|:--|:--|
| `.conf` | Supported |
| `.csc` | Community maintained / unstable |
| `.wip` | Work in progress |
| `.eos` | End of life |
| `.tvb` | TV box |

See `config/boards/README.md` for the full list of variables a board config can set (`BOARD_NAME`, `BOARDFAMILY`, `BOOTCONFIG`, `KERNEL_TARGET`, `DEFAULT_OVERLAYS`, `MODULES*`, `SERIALCON`, …) and `config/sources/families/README.md` for the family / SoC mapping.

## Built With

- **Bash** — `compile.sh` and the entire `lib/` framework
- **Kbuild Makefiles** — kernel device-tree overlay build recipes under `patch/kernel/archive/*/overlay/`
- **Python** — packaging and helper scripts
- **YAML** — GitHub Actions workflows, issue/PR templates, labels, Dependabot, pre-commit, CodeRabbit
- **Debian packaging** — under `packages/` (kernel deb packaging scripts, BSP metapackages)
- **GitHub Actions** — CI, maintenance and data-sync workflows in `.github/workflows/`

## Using as a GitHub Action

`action.yml` exposes this repository as a composite Action ("Rebuild Armbian") for reuse in downstream workflows. Notable inputs include `armbian_target` (`image` or `kernel`), `armbian_board`, `armbian_branch`, `armbian_kernel_branch`, `armbian_release`, `armbian_ui`, `armbian_extensions`, `armbian_compress`, and optional PGP signing (`armbian_pgp_key`, `armbian_pgp_password`). See `action.yml` for the full list and defaults.

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on reporting issues, submitting changes, and contributing code. Development conventions and code-review procedures are covered in the [Development Code Review Procedures and Guidelines](https://docs.armbian.com/Development-Code_Review_Procedures_and_Guidelines/).

Board maintainers are tracked in `.github/CODEOWNERS`, which is regenerated from the upstream contacts database by a scheduled workflow (`.github/workflows/data-sync-maintainers.yml`).

## Resources

- **[Documentation](https://docs.armbian.com/Developer-Guide_Overview/)** — comprehensive guides for building, configuring, and customizing
- **[Website](https://www.armbian.com)** — news, features, and board information
- **[Blog](https://blog.armbian.com)** — development updates and technical articles
- **[Forums](https://forum.armbian.com)** — community support and discussions

## Support

### Community Forums
Get help from users and contributors on troubleshooting, configuration, and development.
👉 [forum.armbian.com](https://forum.armbian.com)

### Real-time Chat
Join discussions with developers and community members on IRC or Discord.
👉 [Community Chat](https://docs.armbian.com/Community_IRC/)

### Paid Consultation
For commercial projects, guaranteed response times, or advanced needs, paid support is available from Armbian maintainers.
👉 [Contact us](https://www.armbian.com/contact)

## License

Distributed under the **GNU General Public License v2** — see [LICENSE](LICENSE).

## Contributors

Thank you to everyone who has contributed to Armbian!

<a href="https://github.com/armbian/build/graphs/contributors">
  <img alt="Contributors" src="https://contrib.rocks/image?repo=armbian/build" />
</a>

## Armbian Partners

Our [partnership program](https://forum.armbian.com/subscriptions) supports Armbian's development and community. Learn more about [our Partners](https://armbian.com/partners).
