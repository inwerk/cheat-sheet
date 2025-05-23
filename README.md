# Cheat Sheet

## Flatpak

### Add Flathub Repositories

```bash
# Add Flathub and Flathub Beta as remote sources
flatpak remote-add --user --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
flatpak remote-add --user --if-not-exists flathub-beta https://flathub.org/beta-repo/flathub-beta.flatpakrepo
```

### Install Additional GNOME Apps

```bash
# [GNOME Boxes](https://apps.gnome.org/Boxes/)
flatpak install flathub org.gnome.Boxes --user --noninteractive --or-update

# [GNOME Videos](https://apps.gnome.org/Totem/)
flatpak install flathub org.gnome.Totem --user --noninteractive --or-update

# [GNOME Resources](https://apps.gnome.org/Resources/)
flatpak install flathub net.nokyan.Resources --user --noninteractive --or-update
```

### Install Other Apps

```bash
# [Anki](https://ankiweb.net)
flatpak install flathub net.ankiweb.Anki --user --noninteractive --or-update

# [Bitwarden](https://bitwarden.com)
flatpak install flathub com.bitwarden.desktop --user --noninteractive --or-update

# [Discord](https://discord.com/)
flatpak install flathub com.discordapp.Discord --user --noninteractive --or-update
flatpak install flathub-beta com.discordapp.DiscordCanary --user --noninteractive --or-update

# [JetBrains IDEs](https://www.jetbrains.com/)
flatpak install flathub com.jetbrains.IntelliJ-IDEA-Ultimate --user --noninteractive --or-update
flatpak install flathub com.jetbrains.PyCharm-Professional --user --noninteractive --or-update
flatpak install flathub com.jetbrains.WebStorm --user --noninteractive --or-update

# [Obsidian](https://obsidian.md/)
flatpak install flathub md.obsidian.Obsidian --user --noninteractive --or-update

# [Raspberry Pi Imager](https://github.com/raspberrypi/rpi-imager/)
flatpak install flathub org.raspberrypi.rpi-imager --user --noninteractive --or-update

# [Signal Desktop](https://signal.org/)
flatpak install flathub org.signal.Signal --user --noninteractive --or-update

# [Thunderbird](https://www.thunderbird.net/)
flatpak install flathub org.mozilla.Thunderbird --user --noninteractive --or-update

# [TeXstudio](https://www.texstudio.org/)
flatpak install flathub org.texstudio.TeXstudio --user --noninteractive --or-update
flatpak install flathub org.freedesktop.Sdk.Extension.texlive//24.08 --user --noninteractive --or-update
```

### Cleanup

```bash
# Remove unused Flatpak runtimes and packages
flatpak uninstall --unused --noninteractive
```

## GNOME Settings

Customize your GNOME desktop and apps using these `gsettings` commands.

### Top Bar Customization

```bash
# Show the date in the top
gsettings set org.gnome.desktop.interface clock-show-date true

# Show the weekday in the top bar
gsettings set org.gnome.desktop.interface clock-show-weekday true

# Show battery percentage in the top bar
gsettings set org.gnome.desktop.interface show-battery-percentage true
```

### File Manager (Nautilus)

```bash
# Set the default view to list-view in Nautilus
gsettings set org.gnome.nautilus.preferences default-folder-viewer 'list-view'
```

### Terminal

```bash
# Set terminal theme to follow system theme
gsettings set org.gnome.Terminal.Legacy.Settings theme-variant 'system'
```

### Text Editor

```bash
# Disable session restore on startup
gsettings set org.gnome.TextEditor restore-session false

# Enable line numbers
gsettings set org.gnome.TextEditor show-line-numbers true

# Disable spell checking
gsettings set org.gnome.TextEditor spellcheck false
```

## rpm-ostree

### Roll Back to the Previous System Version

If a recent update causes issues, you can roll back to the previous deployment:

```bash
sudo rpm-ostree rollback
```

Disable automatic updates too prevent the system from updating to a broken version again:

```bash
sudo systemctl disable rpm-ostreed-automatic.timer
```

Once a new version is safe to use, you can re-enable automatic updates:

```bash
sudo systemctl enable rpm-ostreed-automatic.timer
```

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

Layer the Nextcloud Synchronization Client with rpm-ostree for better integration with Nautilus.

```bash
# Install Nextcloud Synchronization Client
sudo rpm-ostree install nextcloud-client

# Reboot to apply changes
systemctl reboot
```

## toolbx

Here are the toolbx environments I use to isolate development tools.

### Git Environment

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

### Python Environment

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
