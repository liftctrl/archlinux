# SSH Keygen Command Notes

This document collects useful `ssh-keygen` commands for daily work.

---

## 1. Generate SSH Key Pair

Use `ssh-keygen` to create a new SSH key pair for authentication.

### 1.1 Basic RSA Key (Recommended)

Generate a 4096-bit RSA key:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

### 1.2 Modern ED25519 Key

Generate a newer, faster, and more secure ED25519 key:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

### 1.3 Notes

- `-t` → key type (e.g., rsa, ed25519)
- `-b` → key length (4096 for RSA)
- `-C` → comment, usually your email
- The command will prompt for:
  - **File location** (default: ~/.ssh/id_rsa or ~/.ssh/id_ed25519)
  - **Passphrase** (optional, adds extra security)

> Tip: Use ED25519 unless you need RSA for compatibility.

---
