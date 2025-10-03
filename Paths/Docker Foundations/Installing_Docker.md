# 🐳 Docker: Desktop & Installation Guide

## Overview

Containers are built from:

- **Namespaces** → Restrict what processes can see on a system  
- **Control Groups (cgroups)** → Limit resources like memory and CPU  

Since namespaces and cgroups are Linux-specific, Docker runs natively on Linux. Developers using macOS or Windows require Docker Desktop or other workarounds.

---

## Docker Desktop

Docker Desktop provides an easy way to run Docker on **Mac and Windows**:

- Uses a **small, fast VM**:
  - VirtualKit on Mac  
  - Hyper-V on Windows  
- Handles **volume mounts** and **network port exposure** automatically  
- Provides a **GUI** for VM configuration, Kubernetes clusters, and other tasks  

**History:**

- Docker Machine (older solution) used VirtualBox but had:
  - Slower disk and network performance  
  - Required knowledge of VirtualBox CLI (`VBoxManage`)  
- Docker Desktop launched in 2016 to solve these issues  
- In 2021, Mirantis updated licensing:
  - Companies >250 employees and >$10M revenue require a subscription  

---

## Installing Docker on Windows

1. Go to [docker.com](https://www.docker.com/) and download Docker Desktop.  
2. Run the `.exe` file. Confirm publisher is **Docker Inc.**  
3. Select backend:
   - **Hyper-V** → VM-based like Mac  
   - **WSL 2** → Linux running inside Windows; recommended  
4. Configure shortcuts as desired and click **OK**  
5. Wait for installation; restart if prompted  
6. Launch Docker Desktop and accept the **Docker Subscription Service Agreement**  
7. Verify initialization:
   - Status bar: **orange** → initializing, **green** → ready  
   - Taskbar whale icon: moving boxes → starting, still → running  
8. Test Docker in **PowerShell**:
   ```powershell
   docker ps               # List containers
   docker run hello-world  # Pull and run hello-world image

   ---

   # Docker Installation on Linux: Quick Guide

This guide outlines the steps to install the **Docker Engine** and **Docker CLI** on Linux (e.g., Ubuntu), as **Docker Desktop is not required** for native Linux environments.

---

## 🚀 Installation Steps

1.  **Install `cURL`**: Ensure the `cURL` utility is available to download the installation script.
    ```bash
    sudo apt install curl
    ```
    *(Enter your password if prompted.)*

2.  **Download the Installation Script**: Use `cURL` to download the official Docker installation script and save it to `/tmp/get-docker.sh`.
    ```bash
    curl -o /tmp/get-docker.sh [https://get.docker.com](https://get.docker.com)
    ```
    *📝 **Security Note**: It's always recommended to review scripts downloaded from the internet before running them.*

3.  **Run the Installation Script**: Execute the script to install the Docker Engine and CLI. This may take a few minutes.
    ```bash
    sh /tmp/get-docker.sh
    ```
    *A long message output in the terminal confirms a successful installation.*

4.  **Confirm Docker is Working (Initial Test)**: Run the basic `hello-world` container test. This initial run **requires `sudo`**.
    ```bash
    sudo docker run hello-world
    ```

---

## 🛠 Post-Installation Setup (Running Docker without Sudo)

By default, running Docker commands requires `sudo`. To run them as a non-root user, you need to add your user to the **`docker` group**.

1.  **Add Your User to the `docker` Group**:
    * Use the `usermod` command. Replace `linkedin` with your actual username (or use `$USER` for the current user).
    ```bash
    sudo usermod -aG docker linkedin
    # or
    # sudo usermod -aG docker $USER
    ```

2.  **Apply New Permissions**: For the group change to take effect, you would typically need to log out and log back into your system. A quicker way to test is to launch a new shell with the updated group membership:
    ```bash
    sudo -u $USER sh
    ```

3.  **Verify Group Membership (Optional)**: In the new shell, confirm you are now a member of the `docker` group.
    ```bash
    groups
    ```

4.  **Final Confirmation**: Now, test running the `hello-world` container **without `sudo`**.
    ```bash
    docker run hello-world
    ```
    *A successful run indicates you can now use Docker commands without elevated privileges.*

---

## 🔗 Resources

* For distribution-specific instructions and differences, consult the official Docker documentation: `https://docs.docker.io`
