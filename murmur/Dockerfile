FROM alpine:latest
MAINTAINER Chris Spicer <git@cspicer.net>

RUN apk add --no-cache \
    murmur

ENTRYPOINT ["/usr/bin/murmurd"]
CMD ["-fg", "-help"]
