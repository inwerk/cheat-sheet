# Cheat Sheet

## rpm-ostree

### Install Docker

```bash
# Install Docker and Docker Compose
sudo rpm-ostree install moby-engine docker-compose

# Reboot to apply changes
systemctl reboot

# Enable and start Docker service
sudo systemctl enable --now docker.service

# Add your user to the docker group to run docker without sudo
sudo usermod -aG docker $USER
```

After running `usermod`, you need to log out and back in (or reboot) for the group change to take effect.

### Install the Nextcloud Synchronization Client

We need to layer the Nextcloud Synchronization Client with rpm-ostree for better integration with [Nautilus](https://apps.gnome.org/de/Nautilus/).

```bash
# Install Nextcloud Synchronization Client
sudo rpm-ostree install nextcloud-client

# Reboot to apply changes
systemctl reboot
```

## toolbx

Here are the toolbx environments I use to isolate development tools.

### Git

```bash
# Create and enter the Git toolbx
toolbox create git
toolbox enter git

# Update package list
sudo dnf update

# Configure Git credentials
read -p "Enter your GitHub user name: " GITHUB_USERNAME
read -p "Enter your (private) GitHub email: " GITHUB_EMAIL

git config --global user.name "$GITHUB_USERNAME"
git config --global user.email "$GITHUB_EMAIL"

# Install GitHub CLI
sudo dnf install gh
sudo dnf update gh

# Authenticate GitHub CLI
gh auth login

# Exit toolbox
exit
```

### Python

```bash
# Create and enter the Python toolbx
toolbox create python
toolbox enter python

# Update package list
sudo dnf update

# Install the uv Python package manager
curl -LsSf https://astral.sh/uv/install.sh | sh

# Exit toolbox
exit
```
