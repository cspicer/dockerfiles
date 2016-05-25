FROM alpine:3.3
MAINTAINER Chris Spicer <git@cspicer.net>

ENV HUGO_VERSION 0.15
ENV HUGO_ARCHIVE_URL https://github.com/spf13/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_linux_amd64.tar.gz

RUN apk add --no-cache --virtual \
    build-deps \
    curl \
  && curl \
    --silent \
    --show-error \
    --output /tmp/hugo-${HUGO_VERSION}.tar.gz \
    --location ${HUGO_ARCHIVE_URL} \
  && tar -zxf /tmp/hugo-${HUGO_VERSION}.tar.gz -C /tmp \
  && cp -R /tmp/hugo_${HUGO_VERSION}_linux_amd64/hugo_${HUGO_VERSION}_linux_amd64* /usr/local/bin/hugo \
  && rm -rf /tmp/hugo* \
  && apk del build-deps

ENTRYPOINT ["hugo"]
