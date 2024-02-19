# MONAI for Asia/Seoul region

Container images for MONAI Core are available in [loopbackkr's DockerHub repository](https://hub.docker.com/r/loopbackkr/monai). This repository is forked from [docker.io/projectmonai/monai](https://hub.docker.com/r/projectmonai/monai/)

## Quick start

### Docker pulling

`docker pull loopbackkr/monai:latest`

`docker pull loopbackkr/monai:1.3.0`

### Dockerfiling

`FROM loopbackkr/monai:latest`

`FROM loopbackkr/monai:1.3.0`

## Features

* Use [kakao mirror](https://mirror.kakao.com/) reposistory for apt and pip
* Pretty welcome message with version log
* Colorful bash prompt
* Set region to Asia/Seoul for local time
* Preinstalled vim, git, libGL

## References

* [MONAI Core Tutorials](https://github.com/Project-MONAI/tutorials)
* [MONAI Core Docs](https://docs.monai.io/en/stable/)
