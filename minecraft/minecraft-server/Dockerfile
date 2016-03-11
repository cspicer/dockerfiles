FROM alpine:latest
MAINTAINER Chris Spicer <github@cspicer.ca>

ENV MINECRAFT_VERSION 1.9
ENV MINECRAFT_RELEASE_URL "https://s3.amazonaws.com/Minecraft.Download/versions/${MINECRAFT_VERSION}/minecraft_server.${MINECRAFT_VERSION}.jar"

RUN apk add --no-cache \
    curl \
    openjdk7-jre

RUN curl \
    --silent \
    --show-error \
    --location "${MINECRAFT_RELEASE_URL}" \
    --output /tmp/minecraft_server.${MINECRAFT_VERSION}.jar \

