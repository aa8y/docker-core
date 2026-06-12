# Used by every Alpine-based tag (alpine, gradle5, node9/10/11, python2/3).
# Switch base images via `--build-arg BASE_IMAGE=...`; see manifest.yml.
ARG BASE_IMAGE=alpine:3.9
FROM ${BASE_IMAGE}

LABEL org.opencontainers.image.authors="https://github.com/aa8y" \
      org.opencontainers.image.description="Base images intended to be FROM'd by aa8y/* images and used standalone in CI." \
      org.opencontainers.image.licenses="MIT" \
      org.opencontainers.image.source="https://github.com/aa8y/docker-core" \
      org.opencontainers.image.title="aa8y/core" \
      org.opencontainers.image.url="https://hub.docker.com/r/aa8y/core" \
      org.opencontainers.image.vendor="https://github.com/aa8y"

ENV USER docker
ENV USERNAME "Docker User"

# Change to 'root' to do tasks which would require super user privileges.
USER root

# 'bash' is a dependency for many installations.
# 'git' is required by CircleCI for cloning repositories.
# 'openssh' is required by CircleCI for cloning repositories through SSH.
# 'shadow' provides user modification functions which we use.
RUN apk add --no-cache --update \
      bash \
      git \
      openssh \
      shadow && \
    rm -rf /var/cache/apk/*

# Create a 'docker' user because we might not want to run everything as 'root'. Use 9999 as the ID
# to keep it specific and away from the IDs in the host system. Also, lock the user to avoid
# unwanted logins into a Docker container using the 'docker' user as a security measure.
RUN addgroup -g 9999 $USER && \
    adduser -u 9999 -G $USER -g "$USERNAME" -s /bin/bash -D $USER && \
    usermod -L $USER

# Create a 'app' directory to house application specific code when this image or one of its'
# children are being used as a base image for running applications/tests.
ENV APP_DIR /usr/src/app
RUN mkdir -p $APP_DIR && \
    chown -R $USER:$USER $APP_DIR

# Switch to the user 'docker'.
USER $USER
