<div align="center">

# @llm-dev-ops/llm-orchestrator-darwin-x64

<p align="center">
  <strong>Native macOS Intel binary for LLM Orchestrator</strong>
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-darwin-x64"><img src="https://img.shields.io/npm/v/@llm-dev-ops/llm-orchestrator-darwin-x64.svg?style=flat-square" alt="npm version"></a>
  <a href="https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-darwin-x64"><img src="https://img.shields.io/npm/dm/@llm-dev-ops/llm-orchestrator-darwin-x64.svg?style=flat-square" alt="downloads"></a>
  <a href="https://github.com/globalbusinessadvisors/llm-orchestrator/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-Apache--2.0-blue.svg?style=flat-square" alt="License"></a>
  <img src="https://img.shields.io/badge/platform-macOS%20Intel-lightgrey.svg?style=flat-square" alt="Platform">
</p>

</div>

---

## 📦 What is this package?

This package contains the **pre-compiled native binary** of LLM Orchestrator specifically built for **macOS systems with Intel processors (x86_64)**. It is automatically installed as an optional dependency when you install `@llm-dev-ops/llm-orchestrator` on a compatible Intel-based Mac.

### Intel vs Apple Silicon

If you have a Mac with an **M1, M2, M3, or M4** chip, you should use [`@llm-dev-ops/llm-orchestrator-darwin-arm64`](https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-darwin-arm64) instead for better performance.

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
npm install @llm-dev-ops/llm-orchestrator-darwin-x64
```

---

## ⚙️ System Requirements

| Requirement | Minimum | Recommended |
|------------|---------|-------------|
| **OS** | macOS 10.15 (Catalina) | macOS 13+ (Ventura) |
| **Processor** | Intel Core i5 or better | Intel Core i7/i9 |
| **RAM** | 4 GB | 8 GB+ |
| **Disk Space** | 50 MB | 100 MB |
| **Architecture** | x86_64 | x86_64 |

### Compatible Devices

- ✅ **MacBook Pro** - 2013-2020 (Intel models)
- ✅ **MacBook Air** - 2013-2020 (Intel models)
- ✅ **iMac** - 2013-2020 (Intel models)
- ✅ **iMac Pro** - All models
- ✅ **Mac mini** - 2014-2020 (Intel models)
- ✅ **Mac Pro** - 2013-2020

---

## 🔍 Check Your Mac's Processor

Not sure if you have an Intel or Apple Silicon Mac?

```bash
# Check processor type
uname -m

# Intel Mac outputs: x86_64
# Apple Silicon outputs: arm64

# Alternative check
sysctl -n machdep.cpu.brand_string
# Intel shows: "Intel(R) Core(TM) ..."
# Apple Silicon shows: "Apple M1/M2/M3..."
```

Or check via System Information:
1. Click Apple menu () → **About This Mac**
2. Look for **Processor** or **Chip**
   - Intel Mac: Shows "Intel Core i5/i7/i9"
   - Apple Silicon: Shows "Apple M1/M2/M3/M4"

---

## 🎯 Use Cases

Perfect for:

- **Development Machines** - Intel-based MacBook Pro/Air
- **CI/CD** - macOS Intel runners (GitHub Actions, GitLab CI)
- **Testing** - Cross-platform compatibility testing
- **Legacy Systems** - Pre-2020 Mac hardware

---

## 📊 Package Contents

```
@llm-dev-ops/llm-orchestrator-darwin-x64/
├── bin/
│   └── llm-orchestrator          # Native x64 binary (~12 MB)
├── package.json
└── README.md
```

---

## 🔧 Verification

Verify the installation and check the binary:

```bash
# Check installation
npm list -g @llm-dev-ops/llm-orchestrator-darwin-x64

# Verify binary architecture
file $(which llm-orchestrator)
# Output: Mach-O 64-bit executable x86_64

# Check version
llm-orchestrator --version

# Verify CPU architecture
uname -m
# Output: x86_64
```

---

## 🚨 Security Note

### Gatekeeper & Notarization

The binary is **signed and notarized** for macOS Gatekeeper. If you encounter security warnings:

```bash
# Clear quarantine attribute
xattr -d com.apple.quarantine $(which llm-orchestrator)

# Verify signature
codesign -dv $(which llm-orchestrator)
```

---

## 💡 Performance Notes

### Rosetta 2 on Apple Silicon

If you're running this Intel binary on an Apple Silicon Mac via Rosetta 2:

⚠️ **Warning**: You'll experience degraded performance (approximately 70-80% of native speed).

**Recommendation**: Install the native ARM64 version instead:

```bash
npm uninstall -g @llm-dev-ops/llm-orchestrator
arch -arm64 npm install -g @llm-dev-ops/llm-orchestrator
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

# Option 2: Allow in System Preferences
# System Preferences → Security & Privacy → General
# Click "Allow Anyway" next to the blocked message
```
</details>

<details>
<summary><b>Command not found after installation</b></summary>

Ensure npm's bin directory is in your PATH:

```bash
# Add to ~/.zshrc or ~/.bash_profile
export PATH="$(npm bin -g):$PATH"

# Reload shell
source ~/.zshrc  # or source ~/.bash_profile
```
</details>

<details>
<summary><b>Slow performance on M1/M2/M3 Mac</b></summary>

You're likely running the Intel binary via Rosetta 2. Install the native ARM64 version:

```bash
# Check if running via Rosetta
sysctl sysctl.proc_translated
# 1 = Running via Rosetta, 0 = Native

# Install native version
npm uninstall -g @llm-dev-ops/llm-orchestrator
arch -arm64 npm install -g @llm-dev-ops/llm-orchestrator
```
</details>

<details>
<summary><b>Library not loaded errors</b></summary>

Ensure Xcode Command Line Tools are installed:

```bash
xcode-select --install
```
</details>

---

## 🔗 Related Packages

| Package | Platform | npm |
|---------|----------|-----|
| Main Package | All platforms | [@llm-dev-ops/llm-orchestrator](https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator) |
| Linux x64 | Linux x64 | [@llm-dev-ops/llm-orchestrator-linux-x64](https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-linux-x64) |
| Linux ARM64 | Linux ARM64 | [@llm-dev-ops/llm-orchestrator-linux-arm64](https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-linux-arm64) |
| macOS Apple Silicon | macOS ARM64 | [@llm-dev-ops/llm-orchestrator-darwin-arm64](https://www.npmjs.com/package/@llm-dev-ops/llm-orchestrator-darwin-arm64) |

---

## 📄 License

Apache-2.0

---

<div align="center">

**[⬆ back to top](#llm-dev-opsllm-orchestrator-darwin-x64)**

Part of the [LLM Orchestrator](https://github.com/globalbusinessadvisors/llm-orchestrator) project

</div>
