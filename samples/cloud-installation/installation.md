---
layout: default
title: Installation & Configuration
nav_exclude: true
---

# Installation & Configuration

This guide provides instructions for installing the Cloud Data CLI across supported operating systems using package managers, pre-compiled binaries, or Docker containers.

---

## 1. Package Manager Installation

Select the installation command corresponding to your operating system:

### macOS (Homebrew)

Install the CLI binary using Homebrew:

```bash
brew tap clouddata/tools
brew install data-cli

```

### Linux (Debian/Ubuntu)

Add the official APT repository and install the package:

```bash
curl -fsSL [https://packages.clouddata.example.com/gpg](https://packages.clouddata.example.com/gpg) | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/clouddata.gpg
echo "deb [arch=amd64] [https://packages.clouddata.example.com/apt](https://packages.clouddata.example.com/apt) stable main" | sudo tee /etc/apt/sources.list.d/clouddata.list
sudo apt-get update && sudo apt-get install -y data-cli

```

### Docker

Pull and run the official container image:

```bash
docker pull clouddata/data-cli:latest
docker run -rm clouddata/data-cli:latest --version

```

---

## 2. Verifying the Installation

After completing installation, verify that the binary is available in your PATH and check the installed version:

```bash
data-cli --version

```

**Expected output:**

```text
data-cli version 2.14.0 (x86_64-unknown-linux-gnu)

```

---

## 3. Post-Installation Verification

Run the diagnostics utility to verify local dependencies, network accessibility, and TLS handshake protocols:

```bash
data-cli doctor

```

> **Tip:** If `data-cli doctor` returns network timeout warnings, refer to the firewall rules outlined in [Prerequisites](https://www.google.com/search?q=prerequisites.md).

```
