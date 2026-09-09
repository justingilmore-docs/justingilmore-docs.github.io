# Prerequisites & System Requirements

Before installing and configuring the Cloud Data CLI, verify that your environment meets the operating system, dependency, and network access requirements outlined below.

## System Requirements

| Specification | Minimum Requirement | Recommended |
| :--- | :--- | :--- |
| **Operating System** | macOS 12+, Ubuntu 20.04 LTS, RHEL 8+, Windows 11 (WSL2) | Linux / WSL2 preferred |
| **Memory (RAM)** | 2 GB | 4 GB+ |
| **Disk Space** | 250 MB free space | 1 GB free space |
| **Architecture** | `x86_64` or `arm64` | `x86_64` or `arm64` |

---

## Software Dependencies

Ensure the following utilities are installed on your local host prior to binary setup:

* **Curl:** Version `7.68.0` or higher (used for downloading release assets).
* **Git:** Version `2.30.0` or higher (required for configuration tracking).
* **OpenSSL:** Version `1.1.1` or higher (required for secure TLS handshakes).

To verify installed versions, run:
```bash
curl --version
git --version
openssl version
