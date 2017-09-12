# Docker Core

This is a project which would house `Dockerfile`s for base/core images for all the images I build. The idea is to run a few basic steps to make sure the `Dockerfile`s for my other images are DRYer. I try to base all my images on Alpine Linux to have a smaller footprint. So the core images are also based on the same by default. I will add more if the need arises.

## Tags

The tags are `alpine`, `jdk8` and `latest` (same as `alpine`).

## Usage

To be used as a base image for other images.

## License

MIT
