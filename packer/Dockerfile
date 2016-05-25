FROM alpine:latest
MAINTAINER Chris Spicer <git@cspicer.net>

ENV APP_NAME packer
ENV APP_VERSION 0.10.1
ENV APP_ARCHIVE_URL https://releases.hashicorp.com/${APP_NAME}/${APP_VERSION}/${APP_NAME}_${APP_VERSION}_linux_amd64.zip
ENV APP_ARCHIVE_SHA256 eadd33bc0f8fa42034059fc1cda5f43ed6f540746e767480f0706ebed49b45e5

RUN apk add --no-cache \
    curl \
    unzip

RUN curl \
  --silent \
  --show-error \
  --location ${APP_ARCHIVE_URL} \
  --output /tmp/${APP_NAME}_${APP_VERSION}.zip \
  && echo "${APP_ARCHIVE_SHA256SUM} /tmp/${APP_NAME}_${APP_VERSION}.zip" | sha256sum -c . \
  && unzip /tmp/${APP_NAME}_${APP_VERSION}.zip -d /tmp/${APP_NAME} \
  && cp -R /tmp/${APP_NAME}/* /usr/local/bin/ \
  && rm -rf /tmp/${APP_NAME}_${APP_VERSION}.zip /tmp/${APP_NAME}

ENTRYPOINT ["/usr/local/bin/packer"]
