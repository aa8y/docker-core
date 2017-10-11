# Docker Core

This is a project which would house `Dockerfile`s for base/core images for all the images I build. The idea is to run a few basic steps to make sure the `Dockerfile`s for my other images are DRYer. I try to base all my images on Alpine Linux to have a smaller footprint. So the core images are also based on the same by default. I will add more as the need arises.

This image is inspired from `Dockerfile` for the [Instructure Core](https://github.com/instructure/dockerfiles/blob/master/core/Dockerfile) image which is the core image for all [Instructure](https://www.instructure.com/) Docker images. Mine however is a lot less bloated as I designed it to be a bare-minimum base image.

## Tags

The tags are `alpine`, `jdk8`, `python2` and `latest` (same as `alpine`).

## Usage

To be used as a base image for other images.

## License

MIT
