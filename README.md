# Docker installation
## Ubuntu
### References
#### Official
- [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
- [Post-installation steps for Linux](https://docs.docker.com/engine/install/linux-postinstall/)
#### Others
- [Running Docker Containers as Current Host User](https://jtreminio.com/blog/running-docker-containers-as-current-host-user/)

### Remove all previous docker installation
```
sudo apt-get remove docker docker-engine docker.io containerd runc
```

### Set up apt repository
1. Update apt and install some packages
    ```
    sudo apt-get update
    ```
    ```
    sudo apt-get install \
        ca-certificates \
        curl \
        gnupg \
        lsb-release
    ```

2. Add GPG key

    ```
    sudo mkdir -p /etc/apt/keyrings
    ```
    ```
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    ```

3. Set up repository
    ```
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
    | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    ```

### Install Docker Engine
1. Update the `apt` package index again
	```
	sudo apt-get update
	```

	```
	sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
	```

2. Verify installation
	```
	sudo service docker start
	```

	```
	sudo docker run hello-world
	```

### Manage Docker as a non-root user
1. Create `docker` group
	```
	sudo groupadd docker
	```

2. Add current user to the `docker` group 
	```
	sudo usermod -aG docker $USER
	```

3. Activate changes to the groups
	```
	newgrp docker
	```

4. Verify changes -> able to run `hello-world` example without `sudo`
	```
	docker run hello-world
	```

If you encounter issues like
```
docker: Cannot connect to the Docker daemon at unix:///home/<user>/.docker/desktop/docker.sock. Is the docker daemon running?.
```
it is probably because the right docker context is not selected. Execute
```
export DOCKER_HOST=
```
and try again. If it works, include the line above in your `.bashrc` file. See [How to Troubleshoot "Cannot Connect to the Docker Daemon" Error](https://www.howtogeek.com/devops/how-to-troubleshoot-cannot-connect-to-the-docker-daemon-errors/)


### Configure Docker to start on boot

To enable Docker to start on boot use the `systemctl enable` command: 
```
sudo systemctl enable docker.service
```
```
sudo systemctl enable containerd.service
```

To disable docker starting at boot, use `disable` instead
```
sudo systemctl disable docker.service
```
```
sudo systemctl disable containerd.service
```
