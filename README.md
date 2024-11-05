# blolol-filebot-docker

This repository contains Dockerfiles for Blolol's custom FileBot Docker images. A GitHub Action runs daily that rebuilds the images if the base [rednoah/filebot](https://github.com/filebot/filebot-docker) image has changed.

## Images

* `ghcr.io/blolol/filebot-watcher` is built from [`Dockerfile.watcher`](./Dockerfile.watcher) and is based on `rednoah/filebot:watcher`. It adds [jq](https://jqlang.github.io/jq/) to the base image to ease JSON manipulation in post-processing scripts used with the amc script's `--def exec` option.

## Building and pushing locally

To build and push a Docker image locally, you'll need to [authenticate with the GitHub Container Registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry#authenticating-to-the-container-registry) using a personal access token, then use `docker build`:

```sh
echo "$GITHUB_TOKEN" | docker login ghcr.io -u $GITHUB_USERNAME --password-stdin
docker build -f Dockerfile.watcher -t ghcr.io/blolol/filebot-watcher:latest --push .
```
