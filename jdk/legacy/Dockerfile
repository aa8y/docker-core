# Used by the retired JDK 7/8 Alpine tags. Switch via `--build-arg JDK_VERSION=7|8`;
# see manifest.yml. Upstream `openjdk:{7,8}-jdk-alpine3.9` are gone, so we build
# from `alpine:3.9` and install `openjdk${JDK_VERSION}` from Alpine's repositories.
FROM alpine:3.9

ARG JDK_VERSION=8

LABEL org.opencontainers.image.authors="https://github.com/aa8y" \
      org.opencontainers.image.description="Base images intended to be FROM'd by aa8y/* images and used standalone in CI." \
      org.opencontainers.image.licenses="MIT" \
      org.opencontainers.image.source="https://github.com/aa8y/docker-core" \
      org.opencontainers.image.title="aa8y/core" \
      org.opencontainers.image.url="https://hub.docker.com/r/aa8y/core" \
      org.opencontainers.image.vendor="https://github.com/aa8y"

ENV USER docker
ENV USERNAME "Docker User"
ENV JAVA_HOME /usr/lib/jvm/java-1.${JDK_VERSION}-openjdk
ENV PATH $PATH:$JAVA_HOME/bin:$JAVA_HOME/jre/bin

# Change to 'root' to do tasks which would require super user privileges.
USER root

# 'bash' is a dependency for many installations.
# 'git' is required by CircleCI for cloning repositories.
# 'openjdk${JDK_VERSION}' provides the JDK; the upstream 'openjdk:*-jdk-alpine3.9' images were retired.
# 'openssh' is required by CircleCI for cloning repositories through SSH.
# 'shadow' provides user modification functions which we use.
RUN apk add --no-cache --update \
      bash \
      git \
      openjdk${JDK_VERSION} \
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
