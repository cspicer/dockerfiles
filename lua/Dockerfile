FROM alpine:latest
MAINTAINER Chris Spicer

RUN apk add --no-cache \
    lua \
    lua-dev \
    unzip \
  && apk add --no-cache \
    --repository http://dl-3.alpinelinux.org/alpine/edge/testing/ \
    luarocks

RUN apk add --no-cache --virtual build-deps \
    build-base \
    musl-dev \
  && luarocks-5.1 install \
    moonscript \
  && apk del build-deps

VOLUME ["/data"]
ENTRYPOINT ["bash"]

WORKDIR /data

