<div align="center">

# @llm-dev-ops/llm-orchestrator-linux-arm64

<p align="center">
  <strong>Native Linux ARM64 binary for LLM Orchestrator</strong>
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-linux-arm64"><img src="https://img.shields.io/npm/v/@llm-dev-ops/llm-orchestrator-linux-arm64.svg?style=flat-square" alt="npm version"></a>
  <a href="https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-linux-arm64"><img src="https://img.shields.io/npm/dm/@llm-dev-ops/llm-orchestrator-linux-arm64.svg?style=flat-square" alt="downloads"></a>
  <a href="https://github.com/globalbusinessadvisors/llm-orchestrator/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-Apache--2.0-blue.svg?style=flat-square" alt="License"></a>
  <img src="https://img.shields.io/badge/platform-Linux%20ARM64-lightgrey.svg?style=flat-square" alt="Platform">
</p>

</div>

---

## 📦 What is this package?

This package contains the **pre-compiled native binary** of LLM Orchestrator specifically built for **Linux ARM64 (aarch64)** systems. It is automatically installed as an optional dependency when you install `@llm-dev-ops/llm-orchestrator` on a compatible ARM64 Linux system.

### Why ARM64?

ARM64 processors offer:
- 💰 **Cost Efficiency** - AWS Graviton instances are up to 40% cheaper
- ⚡ **Energy Efficiency** - Lower power consumption
- 🚀 **Performance** - Competitive performance per dollar
- 🌍 **Availability** - Growing support across cloud providers

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
npm install @llm-dev-ops/llm-orchestrator-linux-arm64
```

---

## ⚙️ System Requirements

| Requirement | Minimum | Recommended |
|------------|---------|-------------|
| **OS** | Linux (any distribution) | Ubuntu 20.04+, Debian 11+ |
| **Architecture** | ARM64 / aarch64 | ARM64 v8+ |
| **glibc** | 2.31 | 2.35+ |
| **RAM** | 512 MB | 2 GB+ |
| **Disk Space** | 20 MB | 50 MB |

### Compatible Platforms

#### Cloud Providers
- ✅ **AWS Graviton** - EC2 instances (t4g, m6g, c6g, r6g families)
- ✅ **Oracle Cloud** - Ampere A1 instances
- ✅ **Azure** - Dpsv5, Epsv5 series
- ✅ **Google Cloud** - Tau T2A instances
- ✅ **Hetzner** - CAX series

#### Single Board Computers
- ✅ **Raspberry Pi** - 4 Model B, 400, Compute Module 4
- ✅ **Raspberry Pi** - 5
- ✅ **NVIDIA Jetson** - Nano, Xavier NX, AGX
- ✅ **Rock Pi** - 4, 5
- ✅ **Orange Pi** - 5

#### Distributions
- ✅ Ubuntu 20.04, 22.04, 24.04
- ✅ Debian 11, 12
- ✅ Amazon Linux 2023
- ✅ Fedora 36+
- ✅ Arch Linux ARM

---

## 🎯 Use Cases

Perfect for:

- **Cost-Optimized Cloud** - AWS Graviton for 40% cost savings
- **Edge Computing** - Raspberry Pi and edge devices
- **IoT Applications** - ARM-based embedded systems
- **CI/CD Pipelines** - GitHub Actions ARM64 runners
- **Development Boards** - NVIDIA Jetson for AI workloads

---

## 📊 Package Contents

```
@llm-dev-ops/llm-orchestrator-linux-arm64/
├── bin/
│   └── llm-orchestrator          # Native ARM64 binary (~11.5 MB)
├── package.json
└── README.md
```

---

## 🔧 Verification

Verify the installation and check the binary:

```bash
# Check installation
npm list -g @llm-dev-ops/llm-orchestrator-linux-arm64

# Verify architecture
file $(which llm-orchestrator)
# Output: ELF 64-bit LSB executable, ARM aarch64

# Check version
llm-orchestrator --version

# Verify it's native (not emulated)
uname -m
# Output: aarch64
```

---

## 💡 Performance Tips

### AWS Graviton Optimization

```bash
# Use Graviton3 instances for best performance
# Instance types: c7g, m7g, r7g families

# Enable automatic NUMA balancing
echo 1 > /proc/sys/kernel/numa_balancing

# Use local NVMe storage for better I/O
# Instance types: c6gd, m6gd, r6gd
```

### Raspberry Pi Optimization

```bash
# Increase available memory
# Add to /boot/config.txt:
gpu_mem=16

# Use tmpfs for temporary files
export TMPDIR=/tmp/llm-orchestrator
mkdir -p $TMPDIR
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
<summary><b>Installation fails on Raspberry Pi</b></summary>

Ensure you have enough memory and swap:

```bash
# Check available memory
free -h

# Increase swap if needed
sudo dphys-swapfile swapoff
sudo sed -i 's/CONF_SWAPSIZE=.*/CONF_SWAPSIZE=2048/' /etc/dphys-swapfile
sudo dphys-swapfile setup
sudo dphys-swapfile swapon
```
</details>

<details>
<summary><b>GLIBC version errors</b></summary>

Check your glibc version:

```bash
ldd --version

# If too old, consider:
# - Upgrading your distribution
# - Using Docker
docker pull --platform linux/arm64 ghcr.io/globalbusinessadvisors/llm-orchestrator:latest
```
</details>

<details>
<summary><b>Slow performance</b></summary>

Ensure you're running native ARM64, not emulated:

```bash
# Check architecture
uname -m  # Should show: aarch64

# Check if emulated (on x64 systems)
cat /proc/cpuinfo | grep -i "model name"
# Should show ARM processor, not Intel/AMD
```
</details>

---

## 🔗 Related Packages

| Package | Platform | npm |
|---------|----------|-----|
| Main Package | All platforms | [@llm-dev-ops/llm-orchestrator](https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator) |
| Linux x64 | Linux x64 | [@llm-dev-ops/llm-orchestrator-linux-x64](https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-linux-x64) |
| macOS Intel | macOS x64 | [@llm-dev-ops/llm-orchestrator-darwin-x64](https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-darwin-x64) |
| macOS Apple Silicon | macOS ARM64 | [@llm-dev-ops/llm-orchestrator-darwin-arm64](https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-darwin-arm64) |

---

## 📄 License

Apache-2.0

---

<div align="center">

**[⬆ back to top](#llm-dev-opsllm-orchestrator-linux-arm64)**

Part of the [LLM Orchestrator](https://github.com/globalbusinessadvisors/llm-orchestrator) project

</div>
