FROM alpine:latest
MAINTAINER Chris Spicer <github@cspicer.ca>

ENV LIVETAIL_VERSION 1.0
ENV LIVETAIL_RELEASE_URL https://github.com/SumoLogic/livetail-cli/releases/download/v${LIVETAIL_VERSION}/livetail_linux.zip
ENV GLIBC_VERSION 2.23-r1
ENV GLIBC_RELEASE_URL https://github.com/andyshinn/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}

RUN apk add --no-cache \
    ca-certificates \
    curl \
    unzip \
    libgcc

RUN curl \
    --silent \
    --show-error \
    --location "${GLIBC_RELEASE_URL}/glibc-${GLIBC_VERSION}.apk" \
    --output /tmp/glibc-${GLIBC_VERSION}.apk \
  && curl \
    --silent \
    --show-error \
    --location "${GLIBC_RELEASE_URL}/glibc-bin-${GLIBC_VERSION}.apk" \
    --output /tmp/glibc-bin-${GLIBC_VERSION}.apk \
  && apk add --no-cache --allow-untrusted \
    /tmp/glibc-${GLIBC_VERSION}.apk \
    /tmp/glibc-bin-${GLIBC_VERSION}.apk \
  && rm -rf /tmp/glibc*

RUN curl \
    --silent \
    --show-error \
    --location ${LIVETAIL_RELEASE_URL} \
    --output /tmp/livetail_linux.zip \
  && unzip /tmp/livetail_linux.zip -d /tmp/livetail/ \
  && cp -R /tmp/livetail/livetail /usr/local/bin/ \
  && chmod +x /usr/local/bin/livetail \
  && rm -rf /tmp/livetail_linux.zip /tmp/livetail

ENTRYPOINT ["/usr/local/bin/livetail"]