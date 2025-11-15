<div align="center">

# @llm-dev-ops/llm-orchestrator-darwin-arm64

<p align="center">
  <strong>Native macOS Apple Silicon binary for LLM Orchestrator</strong>
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-darwin-arm64"><img src="https://img.shields.io/npm/v/@llm-dev-ops/llm-orchestrator-darwin-arm64.svg?style=flat-square" alt="npm version"></a>
  <a href="https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-darwin-arm64"><img src="https://img.shields.io/npm/dm/@llm-dev-ops/llm-orchestrator-darwin-arm64.svg?style=flat-square" alt="downloads"></a>
  <a href="https://github.com/globalbusinessadvisors/llm-orchestrator/blob/main/LICENSE-MIT"><img src="https://img.shields.io/badge/license-MIT%20OR%20Apache--2.0-blue.svg?style=flat-square" alt="License"></a>
  <img src="https://img.shields.io/badge/platform-macOS%20Apple%20Silicon-lightgrey.svg?style=flat-square" alt="Platform">
  <img src="https://img.shields.io/badge/chip-M1%20|%20M2%20|%20M3%20|%20M4-orange.svg?style=flat-square" alt="Apple Silicon">
</p>

</div>

---

## 📦 What is this package?

This package contains the **pre-compiled native binary** of LLM Orchestrator specifically built for **macOS systems with Apple Silicon processors (M1/M2/M3/M4)**. It is automatically installed as an optional dependency when you install `@llm-dev-ops/llm-orchestrator` on an Apple Silicon Mac.

### Why Apple Silicon?

Apple Silicon offers:
- 🚀 **Superior Performance** - Up to 2x faster than Intel equivalents
- 🔋 **Energy Efficiency** - Exceptional performance per watt
- 💾 **Unified Memory** - Faster memory access and lower latency
- 🎯 **Native Execution** - No Rosetta translation overhead

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
npm install @llm-dev-ops/llm-orchestrator-darwin-arm64
```

### Force ARM64 Installation

If you're on Apple Silicon but getting the x64 version:

```bash
arch -arm64 npm install -g @llm-dev-ops/llm-orchestrator
```

---

## ⚙️ System Requirements

| Requirement | Minimum | Recommended |
|------------|---------|-------------|
| **OS** | macOS 11.0 (Big Sur) | macOS 14+ (Sonoma) |
| **Chip** | Apple M1 | Apple M2 Pro/Max/Ultra, M3/M4 |
| **RAM** | 8 GB | 16 GB+ (32 GB for heavy workloads) |
| **Disk Space** | 50 MB | 100 MB |
| **Architecture** | ARM64 (aarch64) | ARM64 |

### Compatible Devices

- ✅ **MacBook Air** - M1, M2, M3 (2020-2024)
- ✅ **MacBook Pro** - M1, M1 Pro, M1 Max, M2, M2 Pro, M2 Max, M3, M3 Pro, M3 Max (2020-2024)
- ✅ **Mac mini** - M1, M2, M2 Pro (2020-2024)
- ✅ **Mac Studio** - M1 Max, M1 Ultra, M2 Max, M2 Ultra (2022-2024)
- ✅ **iMac** - M1, M3 (2021-2024)
- ✅ **Mac Pro** - M2 Ultra (2023+)

---

## 🔍 Check Your Mac's Chip

Verify you have an Apple Silicon Mac:

```bash
# Check processor type
uname -m
# Apple Silicon outputs: arm64

# Check chip details
sysctl -n machdep.cpu.brand_string
# Shows: "Apple M1/M2/M3/M4..."

# Alternative: Check architecture
arch
# Shows: arm64
```

Or via System Information:
1. Click Apple menu () → **About This Mac**
2. Look for **Chip**: Should show "Apple M1/M2/M3/M4"

---

## 🎯 Use Cases

Perfect for:

- **Development Machines** - MacBook Pro/Air with Apple Silicon
- **Production Workloads** - Mac Studio, Mac Pro
- **CI/CD** - macOS ARM64 runners (GitHub Actions, GitLab CI)
- **High-Performance Computing** - Mac Studio with M1/M2 Ultra
- **Local AI Development** - Leveraging unified memory architecture

---

## 📊 Package Contents

```
@llm-dev-ops/llm-orchestrator-darwin-arm64/
├── bin/
│   └── llm-orchestrator          # Native ARM64 binary (~12 MB)
├── package.json
└── README.md
```

---

## 🔧 Verification

Verify the installation and check the binary:

```bash
# Check installation
npm list -g @llm-dev-ops/llm-orchestrator-darwin-arm64

# Verify binary architecture
file $(which llm-orchestrator)
# Output: Mach-O 64-bit executable arm64

# Check version
llm-orchestrator --version

# Verify native execution (not Rosetta)
sysctl sysctl.proc_translated
# 0 = Native ARM64, 1 = Running via Rosetta

# Check CPU
uname -m
# Output: arm64
```

---

## ⚡ Performance Optimization

### Memory Configuration

Apple Silicon's unified memory architecture provides significant performance benefits:

```bash
# Check available memory
sysctl hw.memsize

# For large workflows, ensure adequate memory:
# M1/M2: 16+ GB recommended
# M1/M2 Pro: 32 GB recommended
# M1/M2 Max/Ultra: 64+ GB for heavy workloads
```

### Concurrency Settings

Apple Silicon excels at parallel workloads:

```bash
# Check CPU cores
sysctl hw.ncpu

# M1: 8 cores (4 performance, 4 efficiency)
# M2: 8 cores (4 performance, 4 efficiency)
# M1 Pro: 8-10 cores
# M1 Max: 10 cores
# M2 Pro: 10-12 cores
# M2 Max: 12 cores
# M1 Ultra: 20 cores
# M2 Ultra: 24 cores

# Optimize concurrency for your chip
llm-orchestrator run workflow.yaml --max-concurrency $(sysctl -n hw.ncpu)
```

### Energy Efficiency

```bash
# Monitor energy usage
sudo powermetrics --samplers cpu_power -i 1000

# Apple Silicon provides excellent performance per watt
# Ideal for long-running LLM workflows
```

---

## 🚨 Security Note

### Gatekeeper & Notarization

The binary is **signed and notarized** for macOS Gatekeeper. If you encounter security warnings:

```bash
# Clear quarantine attribute
xattr -d com.apple.quarantine $(which llm-orchestrator)

# Verify code signature
codesign -dv $(which llm-orchestrator)

# Check notarization
spctl -a -v $(which llm-orchestrator)
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
<summary><b>"Cannot be opened because the developer cannot be verified"</b></summary>

This is a macOS Gatekeeper warning. To bypass:

```bash
# Option 1: Remove quarantine attribute
xattr -d com.apple.quarantine $(which llm-orchestrator)

# Option 2: Allow in System Settings
# System Settings → Privacy & Security
# Scroll down to Security section
# Click "Allow Anyway" next to the blocked message
```
</details>

<details>
<summary><b>Binary runs via Rosetta instead of natively</b></summary>

Ensure you're installing the ARM64 version:

```bash
# Check current architecture
arch
# Should show: arm64

# Force ARM64 installation
arch -arm64 npm uninstall -g @llm-dev-ops/llm-orchestrator
arch -arm64 npm install -g @llm-dev-ops/llm-orchestrator

# Verify native execution
sysctl sysctl.proc_translated
# Should show: 0 (native)
```
</details>

<details>
<summary><b>Command not found after installation</b></summary>

Ensure npm's bin directory is in your PATH:

```bash
# Add to ~/.zshrc
echo 'export PATH="$(npm bin -g):$PATH"' >> ~/.zshrc

# Reload shell
source ~/.zshrc
```
</details>

<details>
<summary><b>Library not loaded errors</b></summary>

Ensure Xcode Command Line Tools are installed:

```bash
xcode-select --install

# Verify installation
xcode-select -p
# Should show: /Library/Developer/CommandLineTools
```
</details>

---

## 💡 Pro Tips

### Optimize for Apple Neural Engine

While this binary doesn't directly use the Neural Engine, you can optimize workflows:

```yaml
# Use local models when possible to leverage ANE
# Configure faster models for simple tasks
providers:
  openai:
    type: openai
    model: gpt-3.5-turbo  # Faster for simple tasks

  claude:
    type: anthropic
    model: claude-3-haiku-20240307  # Cost-effective for analysis
```

### Leverage Unified Memory

```bash
# For workflows with large context windows
# Apple Silicon's unified memory excels here

# M1 Max (64GB): Handle very large contexts
# M1 Ultra (128GB): Process multiple large workflows concurrently
```

---

## 🔗 Related Packages

| Package | Platform | npm |
|---------|----------|-----|
| Main Package | All platforms | [@llm-dev-ops/llm-orchestrator](https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator) |
| Linux x64 | Linux x64 | [@llm-dev-ops/llm-orchestrator-linux-x64](https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-linux-x64) |
| Linux ARM64 | Linux ARM64 | [@llm-dev-ops/llm-orchestrator-linux-arm64](https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-linux-arm64) |
| macOS Intel | macOS x64 | [@llm-dev-ops/llm-orchestrator-darwin-x64](https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-darwin-x64) |

---

## 📄 License

MIT OR Apache-2.0

---

<div align="center">

**[⬆ back to top](#llm-dev-opsllm-orchestrator-darwin-arm64)**

Part of the [LLM Orchestrator](https://github.com/globalbusinessadvisors/llm-orchestrator) project

</div>
