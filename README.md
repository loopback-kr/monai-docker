# MONAI for Asia/Seoul region

Container images for MONAI Core are available in [loopbackkr's DockerHub repository](https://hub.docker.com/r/loopbackkr/pytorch). This repository is forked from [docker.io/projectmonai/monai](https://hub.docker.com/r/projectmonai/monai/)

## Quick start

### Docker pulling

`docker pull loopbackkr/monai:latest`

`docker pull loopbackkr/monai:1.1.0`

### Dockerfiling

`FROM loopbackkr/monai:latest`

`FROM loopbackkr/monai:1.1.0`

## Features

* Use [kakao mirror](https://mirror.kakao.com/) reposistory for apt and pip
* Pretty welcome message with version log
* Colorful bash prompt
* preinstalled vim, git

## References

* [MONAI Core Tutorials](https://github.com/Project-MONAI/tutorials)
* [MONAI Core Docs](https://docs.monai.io/en/stable/)
