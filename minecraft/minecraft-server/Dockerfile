FROM alpine:latest
MAINTAINER Chris Spicer <git@cspicer.net>

ENV MINECRAFT_VERSION 1.9.4
ENV MINECRAFT_RELEASE_URL "https://s3.amazonaws.com/Minecraft.Download/versions/${MINECRAFT_VERSION}/minecraft_server.${MINECRAFT_VERSION}.jar"

ENV MINECRAFT_MEMORY_MIN 2048
ENV MINECRAFT_MEMORY_MAX 4096

RUN apk add --no-cache \
    curl \
    openjdk8-jre-base

RUN mkdir -p /data/minecraft \
  && curl \
    --silent \
    --show-error \
    --location "${MINECRAFT_RELEASE_URL}" \
    --output /data/minecraft/server.jar

COPY run.sh /data/minecraft/run.sh
WORKDIR /data/minecraft/server

ENTRYPOINT ["/data/minecraft/run.sh"]

