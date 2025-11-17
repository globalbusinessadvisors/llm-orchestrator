<div align="center">

# @llm-dev-ops/llm-orchestrator-linux-x64

<p align="center">
  <strong>Native Linux x64 binary for LLM Orchestrator</strong>
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-linux-x64"><img src="https://img.shields.io/npm/v/@llm-dev-ops/llm-orchestrator-linux-x64.svg?style=flat-square" alt="npm version"></a>
  <a href="https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-linux-x64"><img src="https://img.shields.io/npm/dm/@llm-dev-ops/llm-orchestrator-linux-x64.svg?style=flat-square" alt="downloads"></a>
  <a href="https://github.com/globalbusinessadvisors/llm-orchestrator/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-Apache--2.0-blue.svg?style=flat-square" alt="License"></a>
  <img src="https://img.shields.io/badge/platform-Linux%20x64-lightgrey.svg?style=flat-square" alt="Platform">
</p>

</div>

---

## 📦 What is this package?

This package contains the **pre-compiled native binary** of LLM Orchestrator specifically built for **Linux x64 (x86_64)** systems. It is automatically installed as an optional dependency when you install `@llm-dev-ops/llm-orchestrator` on a compatible Linux system.

### Why platform-specific packages?

Platform-specific packages ensure you get:
- ✅ **Optimal Performance** - Native compilation for your architecture
- ✅ **Zero Dependencies** - No need for build tools or compilers
- ✅ **Instant Installation** - Pre-built binaries install in seconds
- ✅ **Smaller Downloads** - Only download what you need

---

## 🚀 Installation

### Automatic (Recommended)

Simply install the main package - this platform package will be installed automatically:

```bash
npm install -g @llm-dev-ops/llm-orchestrator
```

### Manual (Advanced)

If you need to install this package directly:

```bash
npm install @llm-dev-ops/llm-orchestrator-linux-x64
```

---

## ⚙️ System Requirements

| Requirement | Minimum | Recommended |
|------------|---------|-------------|
| **OS** | Linux (any distribution) | Ubuntu 20.04+, Debian 11+, RHEL 8+ |
| **Architecture** | x86_64 (64-bit) | x86_64 |
| **glibc** | 2.31 | 2.35+ |
| **RAM** | 512 MB | 2 GB+ |
| **Disk Space** | 20 MB | 50 MB |

### Compatible Distributions

- ✅ Ubuntu 20.04, 22.04, 24.04
- ✅ Debian 11, 12
- ✅ RHEL / Rocky Linux / AlmaLinux 8, 9
- ✅ Fedora 36+
- ✅ openSUSE Leap 15+
- ✅ Arch Linux
- ✅ Alpine Linux 3.17+ (with glibc compatibility layer)

---

## 🎯 Use Cases

Perfect for:

- **CI/CD Pipelines** - GitHub Actions, GitLab CI, Jenkins
- **Docker Containers** - Standard x64 containers
- **Cloud Servers** - AWS EC2 (t3/m5/c5), DigitalOcean, Linode
- **Development Machines** - Linux workstations and laptops
- **Production Servers** - Traditional x64 infrastructure

---

## 📊 Package Contents

```
@llm-dev-ops/llm-orchestrator-linux-x64/
├── bin/
│   └── llm-orchestrator          # Native x64 binary (~11.5 MB)
├── package.json
└── README.md
```

---

## 🔧 Verification

Verify the installation and check the binary:

```bash
# Check installation
npm list -g @llm-dev-ops/llm-orchestrator-linux-x64

# Verify binary
file $(which llm-orchestrator)
# Output: ELF 64-bit LSB executable, x86-64

# Check version
llm-orchestrator --version
```

---

## 📚 Documentation

For complete usage documentation, see the main package:

- **Main Package**: [@llm-dev-ops/llm-orchestrator](https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator)
- **GitHub Repository**: [llm-orchestrator](https://github.com/globalbusinessadvisors/llm-orchestrator)
- **API Documentation**: [docs.rs](https://docs.rs/llm-orchestrator)

---

## 🐛 Troubleshooting

<details>
<summary><b>Binary not found after installation</b></summary>

Ensure npm's bin directory is in your PATH:

```bash
export PATH="$(npm bin -g):$PATH"
```
</details>

<details>
<summary><b>GLIBC version errors</b></summary>

Check your glibc version:

```bash
ldd --version

# If too old, consider:
# - Upgrading your distribution
# - Using the Docker image instead
docker pull ghcr.io/globalbusinessadvisors/llm-orchestrator:latest
```
</details>

<details>
<summary><b>Permission denied errors</b></summary>

Make the binary executable:

```bash
chmod +x $(which llm-orchestrator)
```
</details>

---

## 🔗 Related Packages

| Package | Platform | npm |
|---------|----------|-----|
| Main Package | All platforms | [@llm-dev-ops/llm-orchestrator](https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator) |
| Linux ARM64 | Linux ARM64 | [@llm-dev-ops/llm-orchestrator-linux-arm64](https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-linux-arm64) |
| macOS Intel | macOS x64 | [@llm-dev-ops/llm-orchestrator-darwin-x64](https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-darwin-x64) |
| macOS Apple Silicon | macOS ARM64 | [@llm-dev-ops/llm-orchestrator-darwin-arm64](https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-darwin-arm64) |

---

## 📄 License

Apache-2.0

---

<div align="center">

**[⬆ back to top](#llm-dev-opsllm-orchestrator-linux-x64)**

Part of the [LLM Orchestrator](https://github.com/globalbusinessadvisors/llm-orchestrator) project

</div>
