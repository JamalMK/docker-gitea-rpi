# Gitea on Raspberry Pi
This image hosts [Gitea](https://gitea.io) in a Raspberry Pi docker image of minimal size, yet fully functional.

This work is a fork of [kapdap/gitea-rpi](https://hub.docker.com/r/kapdap/gitea-rpi), but with a slightly smaller image.

## Tags
|Tag Style|Meaning|
|--|--|
|latest|Will always contain the newest image|
|latest-x.x|Will contain the newest image limited to Gitea version x.x. Use this if you want to take security updates but no new features.|
|stable|Will contain the newest stable image|
|x.x.x-y|Contains image version y with Gitea version x.x.x.

## Usage
In order to ensure that your data and configuration for Gitea remain in place after container restarts and updates, a volume must be created within Docker. To create a Docker volume, use the command below which creates a docker volume on your system called ```gitea```.

```bash
docker volume create gitea
```
Then run the Gitea Container in Docker with the command below:
```bash
docker run -d -p 2222:22 -p 3000:3000 -v gitea:/data patrickthedev/gitea-rpi
```
The above command is broken down below:

| -p 3000:3000            | Exposes port 3000 and maps it to Port 3000 on the container.                   |
|-------------------------|--------------------------------------------------------------------------------|
| -p 2222:22              | Exposes port 2222 on the host and maps it to Port 22 on the container.         |
| -v gitea:/data          | Maps the docker volume named gitea to /data within the container.              |
| --restart always        | Will ensure that the container restarts if it is every stopped for any reason. |
| patrickthedev/gitea-rpi | The image from [Docker Hub](https://hub.docker.com/r/patrickthedev/gitea-rpi). |

## Other Random Notes

I had to specify ports as ```2222:22``` instead of ```22:22``` because I am using SSH via port 22 to access the actual machine itself.

Since the docker image is Alpine based, use ```apk add emacs``` to install a decent editor within the container.

Good additional info on Gitea + Docker here: https://docs.gitea.io/en-us/install-with-docker/
