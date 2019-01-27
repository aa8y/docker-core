FROM ubuntu:bionic

MAINTAINER Arun Allamsetty <arun.allamsetty@gmail.com>

ENV USER docker
ENV USERNAME "Docker User"

# Change to 'root' to do tasks which would require super user privileges.
USER root

# APT setup
ENV DEBIAN_FRONTEND=noninteractive
# 'git' is required by CircleCI for cloning repositories.
# 'openssh-server' is required by CircleCI for cloning repositories through SSH.
# 'software-properties-common' lets you run 'apt-add-repository' which would probably be needed by
#  images which use this image.
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
      git \
      openssh-server \
      software-properties-common && \
    apt-get clean && \
    rm -rf \
      /tmp/* \
      /var/lib/apt/lists/* \
      /var/tmp/

# Create a 'docker' user because we might not want to run everything as 'root'. Use 9999 as the ID
# to keep it specific and away from the IDs in the host system. Also, lock the user to avoid
# unwanted logins into a Docker container using the 'docker' user as a security measure.
RUN addgroup --gid 9999 $USER && \
    adduser --uid 9999 --gid 9999 --disabled-password --gecos "$USERNAME" --shell /bin/bash $USER && \
    usermod -L $USER

# Create a 'app' directory to house application specific code when this image or one of its'
# children are being used as a base image for running applications/tests.
ENV APP_DIR /usr/src/app
RUN mkdir -p $APP_DIR && \
    chown -R $USER:$USER $APP_DIR

# Switch to the user 'docker'.
USER $USER
