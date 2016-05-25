FROM alpine:latest
MAINTAINER Chris Spicer <git@cspicer.net>

ENV APP_NAME vault
ENV APP_VERSION 0.5.2
ENV ARCHIVE_URL https://releases.hashicorp.com/${APP_NAME}/${APP_VERSION}/${APP_NAME}_${APP_VERSION}_linux_amd64.zip

RUN apk add --update \
  bash \
  ca-certificates \
  curl \
  unzip

RUN curl -sSL ${ARCHIVE_URL} -o /tmp/${APP_NAME}_${APP_VERSION}.zip \
  && unzip /tmp/${APP_NAME}_${APP_VERSION}.zip -d /tmp/${APP_NAME} \
  && cp -R /tmp/${APP_NAME}/* /usr/local/bin \
  && rm -rf /tmp/${APP_NAME}_${APP_VERSION}.zip /tmp/${APP_NAME}

ENTRYPOINT ["/usr/local/bin/vault"]
