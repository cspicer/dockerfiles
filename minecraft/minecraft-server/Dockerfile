FROM alpine:latest
MAINTAINER Chris Spicer <github@cspicer.ca>

ENV MINECRAFT_VERSION 1.9.2
ENV MINECRAFT_RELEASE_URL "https://s3.amazonaws.com/Minecraft.Download/versions/${MINECRAFT_VERSION}/minecraft_server.${MINECRAFT_VERSION}.jar"

RUN apk add --no-cache \
    curl \
    openjdk8-jre-base

RUN mkdir -p /data/minecraft \
  && curl \
    --silent \
    --show-error \
    --location "${MINECRAFT_RELEASE_URL}" \
    --output /data/minecraft/server.jar

WORKDIR /data/minecraft

ENTRYPOINT ["/usr/bin/java"]
CMD ["-Xmx2048M", "-Xms1024M", "-XX:+UseConcMarkSweepGC", "-jar", "server.jar"]
