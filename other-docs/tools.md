Here is the **simplest and correct way** to install **WSL (Windows Subsystem for Linux)** on Windows 10 or Windows 11.

---

# ✅ **Method 1: Easy Method — Install WSL with One Command**

Open **PowerShell (Run as Administrator)** and run:

```powershell
wsl --install
```

This will:

✔ Enable WSL
✔ Install *Ubuntu* by default
✔ Install the latest WSL kernel
✔ Restart your system if needed

After reboot → it will ask you to create a Linux username & password.

---

# ✅ **Method 2: Install Specific Linux Distro**

List available distros:

```powershell
wsl --list --online
```

Install a specific one:

```powershell
wsl --install -d Ubuntu-22.04
```

---

# ✅ **Method 3: If WSL is disabled on your system**

Enable features manually:

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

Then install kernel:

```powershell
wsl --update
```

Set WSL2 as default:

```powershell
wsl --set-default-version 2
```

---

# 🚀 Verify WSL Installation

```powershell
wsl --version
```

Start Ubuntu:

```powershell
wsl
```

---

# 🎯 Optional Useful Commands

### Set default distro:

```powershell
wsl -s Ubuntu
```

### View installed distros:

```powershell
wsl --list --verbose
```



