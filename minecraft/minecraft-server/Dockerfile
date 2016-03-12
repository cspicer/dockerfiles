FROM alpine:latest
MAINTAINER Chris Spicer <github@cspicer.ca>

ENV MINECRAFT_VERSION 1.9
ENV MINECRAFT_RELEASE_URL "https://s3.amazonaws.com/Minecraft.Download/versions/${MINECRAFT_VERSION}/minecraft_server.${MINECRAFT_VERSION}.jar"

RUN apk add --no-cache \
    curl \
    openjdk8-jre-base

RUN mkdir -p /opt/minecraft \
  && curl \
    --silent \
    --show-error \
    --location "${MINECRAFT_RELEASE_URL}" \
    --output /opt/minecraft/server.jar

WORKDIR /data
VOLUME /data

RUN echo eula=true > /data/eula.txt
COPY server.properties /data/
