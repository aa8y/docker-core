FROM alpine:3.6

MAINTAINER Arun Allamsetty <arun.allamsetty@gmail.com>

# Install bash as many installations require bash to run.
RUN apk add --no-cache --update bash && \
    rm -rf /var/cache/apk/*

# Create a 'docker' user because we might not want to run everything as 'root'. Use 9999 as the ID
# to keep it specific and away from the IDs in the host system.
RUN addgroup -g 9999 docker && \
    adduser -u 9999 -G docker -g "Docker User" -s /bin/bash -D docker

RUN apk add --no-cache --update shadow && \
    usermod -L docker && \
    apk del --purge shadow && \
    rm -rf /var/cache/apk/*

# Switch to the user 'docker'.
USER docker
