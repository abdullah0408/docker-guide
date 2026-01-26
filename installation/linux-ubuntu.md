# Install using the apt repository
Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker apt repository. Afterward, you can install and update Docker from the repository.

Official Docs: https://docs.docker.com/engine/install/ubuntu

## Set up Docker's apt repository

### Add Docker's official GPG key:

```bash
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

### Add the repository to Apt sources:

```bash
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt update
```

## Install the Docker packages

To install the latest version, run:

```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## Verify that Docker is installed correctly by checking the version:
```bash
docker --version
# Docker version 26.x.x, build xxxxxxx
```

**Note**  
The Docker service starts automatically after installation. To verify that Docker is running, use:

```bash
sudo systemctl status docker
```

⚠️ Some systems may have this behavior disabled and will require a manual start:

```bash
sudo systemctl start docker
```

### (Optional) Run Docker without `sudo`

By default, Docker commands require `sudo`. To allow your user to run Docker commands without `sudo`, add your user to the `docker` group:

```bash
sudo usermod -aG docker $USER
newgrp docker
```

⚠️ If `newgrp` does not take effect, log out and log back in, then try again.

## Verify that the installation is successful by running the hello-world image:

```bash
sudo docker run hello-world
```

This command downloads a test image and runs it in a container. When the container runs, it prints a confirmation message and exits.

You have now successfully installed and started Docker Engine.

## Uninstall Docker Engine

Uninstall the Docker Engine, CLI, containerd, and Docker Compose packages:

```bash
sudo apt purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras
```

Images, containers, volumes, or custom configuration files on your host aren't automatically removed. To delete all images, containers, and volumes:

```bash
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

Remove source list and keyrings

```bash
sudo rm /etc/apt/sources.list.d/docker.sources
sudo rm /etc/apt/keyrings/docker.asc
```

You have to delete any edited configuration files manually.
