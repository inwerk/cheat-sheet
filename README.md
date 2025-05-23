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

Layering the Nextcloud Synchronization Client with rpm-ostree for better integration with [Nautilus](https://apps.gnome.org/de/Nautilus/).

```bash
# Install Nextcloud Synchronization Client
sudo rpm-ostree install nextcloud-client

# Reboot to apply changes
systemctl reboot
```
