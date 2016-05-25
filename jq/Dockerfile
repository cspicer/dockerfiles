FROM alpine:latest
MAINTAINER Chris Spicer <git@cspicer.net>

RUN apk add --update \
    bash \
    jq \
  && rm -rf /var/cache/apk/*

ENTRYPOINT ["jq"]
