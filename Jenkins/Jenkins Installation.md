# Jenkins Installation

# Jenkins Installation Guide for Linux (Debian/Ubuntu)

This guide provides detailed steps to install Jenkins on **Debian** and **Ubuntu** systems using the `apt` package manager. It includes both **Long-Term Support (LTS)** and **Weekly** release installation options.

---

## 📋 Prerequisites

### ✅ Hardware Requirements

- **Minimum**:
  - 256 MB RAM
  - 1 GB disk space (10 GB if using Docker)
- **Recommended for a small team**:
  - 4 GB+ RAM
  - 50 GB+ disk space
- **Comprehensive details**: [Hardware Recommendations](https://www.jenkins.io/doc/book/installing/#hardware-recommendations)

### ✅ Software Requirements

- **Java**: Required before installing Jenkins.
  - Recommended: OpenJDK 21
  - See [Java Requirements](https://www.jenkins.io/doc/administration/requirements/java/)
- **Web Browser**: See [Web Browser Compatibility](https://www.jenkins.io/doc/book/installing/#web-browser-compatibility)
- **Linux OS Support**: [Linux Support Policy](https://www.jenkins.io/doc/administration/requirements/linux/)
- **Systemd Support** (required for newer versions): [Managing systemd services](https://www.jenkins.io/doc/book/installing/linux/#using-systemd)

---

## ☕ Step 1: Install Java (OpenJDK 21)

Before installing Jenkins, ensure that Java is installed. Jenkins requires Java to run, and installing it **before** Jenkins avoids startup issues.

```bash
sudo apt update
sudo apt install fontconfig openjdk-21-jre

Verify Java installation:

java -version


Expected output:

openjdk version "21.0.3" 2024-04-16
OpenJDK Runtime Environment (build 21.0.3+11-Debian-2)
OpenJDK 64-Bit Server VM (build 21.0.3+11-Debian-2, mixed mode, sharing)

📦 Step 2: Install Jenkins

You can choose to install either the Long-Term Support (LTS) release or the Weekly release.

🔁 Option A: Install Jenkins LTS (Recommended for Production)
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/" | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install jenkins

🚀 Option B: Install Jenkins Weekly (Latest Features & Bug Fixes)
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian/jenkins.io-2023.key

echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/" | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install jenkins

⚙️ Service Setup and Systemd Configuration

Jenkins is configured as a systemd service since version 2.332.1+.

After installation:

A jenkins user is created.

Jenkins runs as a background service.

Logs are sent to systemd-journald.

Jenkins listens on port 8080 by default.

To view Jenkins service logs:

journalctl -u jenkins.service


To inspect the systemd service:

systemctl cat jenkins


To change the default port (e.g., to 8081):

sudo systemctl edit jenkins


Add the following in the editor:

[Service]
Environment="JENKINS_PORT=8081"


Reload the systemd daemon and restart Jenkins:

sudo systemctl daemon-reexec
sudo systemctl restart jenkins

🌐 Access Jenkins

After installation, Jenkins will be available at:

http://<your-server-ip>:8080

🧑‍💻 Why Use apt Instead of apt-get?

While apt-get remains functional, apt provides a more user-friendly command structure and better output formatting. For general package management tasks (install, remove, search), apt is preferred.

📚 Additional Links

Jenkins Official Documentation

Linux Support Policy

Servlet Container Support

Windows Support Policy

🧾 License

This documentation is based on the official Jenkins installation guide
. Jenkins is an open-source automation server under the MIT license.