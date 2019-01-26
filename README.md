# Docker Core

[![Build Status](https://travis-ci.org/aa8y/docker-core.svg?branch=master)](https://travis-ci.org/aa8y/docker-core)

This is a project which would house `Dockerfile`s for base/core images for (almost) all the images under the `aa8y/` namespace. The idea is to DRY out common steps between those images and also add steps which make the official images, from which the core images are built, more usable. Alpine Linux is the root base image of choice owing to its smaller footprint. But more conventional base images might be built if the need arises in the future.

This image is inspired from `Dockerfile` for the [Instructure Core](https://github.com/instructure/dockerfiles/blob/master/core/latest/Dockerfile) image which is the core image for all [Instructure](https://www.instructure.com/) Docker images. The [`aa8y/core`](https://hub.docker.com/r/aa8y/core/) are less bloated however given the bare-minimum design.

## Tags

Tags are built from various Alpine based official images.

|        | Tags                        |
|--------|-----------------------------|
| Alpine | `alpine`, `latest`          |
| Gradle | `gradle5`                   |
| Java   | `jdk7`, `jdk8`              |
| NodeJS | `node9`, `node10`, `node11` |
| Python | `python2`, `python3`        |
| Ubuntu | `ubuntu`                    |

## Usage

To be used as a base image for other images or as standalone images in CI environments.

## License

MIT
