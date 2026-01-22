# docker/docker-install
Home of the script that lives at `get.docker.com` and `test.docker.com`!

The purpose of the install script is for a convenience for quickly
installing the latest Docker-CE releases on the supported linux
distros. It is not recommended to depend on this script for deployment
to production systems. For more thorough instructions for installing
on the supported distros, see the [install
instructions](https://docs.docker.com/engine/installation/).

This repository is solely maintained by Docker, Inc.

## Usage:

1. Update and upgrade

```
sudo apt update -y

sudo apt upgrade -y

sudo apt install curl -y

```

Or

```
sudo apt update -y && sudo apt upgrade -y && sudo apt install curl -y
```

2. Install docker
3. 
From `https://get.docker.com`:
```shell
curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh
```

From `https://test.docker.com`:
```shell
curl -fsSL https://test.docker.com -o test-docker.sh
sh test-docker.sh
sudo usermod -aG docker your-user
```
3. Configure
OSError: inotify watch limit reached:
```shell

cat /proc/sys/fs/inotify/max_user_watches
8192
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```
Error
```shell
sh install.sh

docker ps

sudo chmod 666 /var/run/docker.sock

```
## II. Docker compose

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version

```
### Command
```
docker-compose up|start|stop|down
```

## Testing:

To verify that the install script works amongst the supported operating systems run:

```shell
make check
```

## Update docker-compose
```
	sudo rm /usr/local/bin/docker-compose			# (Nếu muốn giữ lại để dùng song song thì có thể bỏ qua bước này.)
```
Nếu không có docker cũ
```
	mkdir -p ~/.docker/cli-plugins/
	curl -SL https://github.com/docker/compose/releases/latest/download/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose
	chmod +x ~/.docker/cli-plugins/docker-compose
	docker compose version
	sudo ln -s ~/.docker/cli-plugins/docker-compose /usr/local/bin/docker-compose
	sudo rm /usr/local/bin/docker-compose
	docker compose up
	docker-compose up

```

## Docker compose v2
Sử dụng GO
Tải xuống Binary: Thay thế <VERSION> bằng phiên bản Compose V2 mới nhất (ví dụ: 2.23.3 - hãy kiểm tra trang GitHub chính thức để có phiên bản mới nhất).
```
DOCKER_CONFIG=${DOCKER_CONFIG:-$HOME/.docker}
mkdir -p $DOCKER_CONFIG/cli-plugins
curl -SL https://github.com/docker/compose/releases/download/v<VERSION>/docker-compose-linux-x86_64 -o $DOCKER_CONFIG/cli-plugins/docker-compose

chmod +x $DOCKER_CONFIG/cli-plugins/docker-compose

docker compose version
```


## Clear log:
```
docker ps -q --no-trunc
or

docker inspect -f '{{.Id}}' <container_name_or_id>

sudo sh -c 'truncate -s 0 /var/lib/docker/containers/a1b2c3d4e5f67890.../a1b2c3d4e5f67890...-json.log'
```

## Legal
*Brought to you courtesy of our legal counsel. For more context,
please see the [NOTICE](NOTICE) document in this repo.*

Use and transfer of Docker may be subject to certain restrictions by the
United States and other governments.

It is your responsibility to ensure that your use and/or transfer does not
violate applicable laws.

For more information, please see https://www.bis.doc.gov

## Reporting security issues

The maintainers take security seriously. If you discover a security issue,
please bring it to their attention right away!

Please **DO NOT** file a public issue, instead send your report privately to
[security@docker.com](mailto:security@docker.com).

Security reports are greatly appreciated and we will publicly thank you for it.
We also like to send gifts—if you're into Docker schwag, make sure to let
us know. We currently do not offer a paid security bounty program, but are not
ruling it out in the future.

## Licensing

docker/docker-install is licensed under the Apache License, Version 2.0.
See [LICENSE](LICENSE) for the full license text.
