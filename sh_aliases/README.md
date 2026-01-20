# Setup global aliases

To automatically source the aliases, add them in your .bashrc, .profile or .zshrc file:

```bash
$ echo ". ~/<path-to-sh-aliases>/sh_aliases.v3" >> ~/.bashrc
# or
$ echo ". ~/<path-to-sh-aliases>/sh_aliases.v3" >> ~/.profile
# or
$ echo "source ~/<path-to-sh-aliases>/sh_aliases.v3" >> ~/.zshrc
```

# Setup for Windows

In order to setup docker and the aliases on windows, you should setup WSL and install Docker desktop.

## Setting up WSL (Windows Subsystem for Linux) on Windows

To run this project in a Linux-like environment on Windows, we recommend setting up WSL (Windows Subsystem for Linux). Follow the steps below to install and configure it:

### 1. Enable WSL and Virtual Machine Platform

Open **PowerShell as Administrator** and run:

```powershell
wsl --install
```

This command will:

- Enable the necessary Windows features
- Install the latest WSL version
- Download and install Ubuntu (by default)

> **Note**: If you're using an older version of Windows or `wsl --install` doesn't work, follow the manual [installation guide](https://learn.microsoft.com/en-us/windows/wsl/install-manual).

### 2. Restart Your Computer

After the installation, restart your PC to complete the setup.

### 3. Launch WSL

Once your system reboots, open **Ubuntu** (or your preferred distribution) from the Start menu.
The first time you launch it, you’ll be prompted to create a new UNIX username and password.

### 4. Update and Upgrade Packages

Once inside the WSL terminal, update your package list and upgrade installed packages:

```bash
sudo apt update && sudo apt upgrade -y
```

## Setting up Docker Desktop with WSL 2 on Windows

To use Docker on Windows within a WSL 2 environment, follow these steps to install and configure Docker Desktop.

### 1. Install Docker Desktop for Windows

Download and install Docker Desktop from the official website:

👉 [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)

> **Note**: Docker Desktop requires:
>
> - Windows 10 64-bit: Pro, Enterprise, or Education (Build 19044 or higher), or Windows 11
> - WSL 2 feature enabled

### 2. Enable WSL 2 and Install a Linux Distribution

If you haven’t already set up WSL 2, follow the steps in the "Setting up WSL" section above.

You can check your WSL version with:

```powershell
wsl --list --verbose
```

If your distro is still on WSL 1, convert it using:

```powershell
wsl --set-version <distro-name> 2
```

Example:

```powershell
wsl --set-version Ubuntu 2
```

### 3. Start Docker Desktop

Once Docker Desktop is installed, launch it from the Start menu.
Docker will automatically detect WSL 2 distributions and integrate with them.

### 4. Enable Integration with Your WSL Distro

In Docker Desktop:

- Open **Settings** > **Resources** > **WSL Integration**
- Enable Docker for your installed WSL distributions (e.g., `Ubuntu`)
- Click Apply & Restart

### 5. Test Docker Inside WSL

Now you can open your WSL terminal (e.g. Ubuntu) and test Docker:

```bash
docker --version
docker run hello-world
```

If everything is configured correctly, you should see a confirmation message from Docker.
