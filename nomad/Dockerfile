FROM alpine:latest
MAINTAINER Chris Spicer <git@cspicer.net>

ENV NOMAD_VERSION 0.3.2
ENV NOMAD_ARCHIVE_URL https://releases.hashicorp.com/nomad/${NOMAD_VERSION}/nomad_${NOMAD_VERSION}_linux_amd64.zip
ENV NOMAD_ARCHIVE_SHA256SUM 710ff3515bc449bc2a06652464f4af55f1b76f63c77a9048bc30d6fde284b441

ENV GLIBC_VERSION 2.23-r1
ENV GLIBC_RELEASE_URL https://github.com/andyshinn/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}
ENV GLIBC_KEY_URL https://raw.githubusercontent.com/andyshinn/alpine-pkg-glibc/master/andyshinn.rsa.pub
ENV GLIBC_KEY_PATH /etc/apk/keys/andyshinn.rsa.pub

RUN apk add --no-cache  \
    curl \
    ca-certificates \
    unzip \
    libgcc

RUN curl \
    --silent \
    --show-error \
    --location ${GLIBC_KEY_URL} \
    --output ${GLIBC_KEY_PATH} \
  && curl \
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
  && rm -rf /tmp/glibc* \
  && rm ${GLIBC_KEY_PATH}

RUN curl \
    --silent \
    --show-error \
    --location "${NOMAD_ARCHIVE_URL}" \
    --output /tmp/nomad.zip \
  && echo "${NOMAD_ARCHIVE_SHA256SUM} /tmp/nomad.zip" | sha256sum -c . \
  && unzip /tmp/nomad.zip -d /tmp/nomad \
  && cp -R /tmp/nomad/* /usr/local/bin \
  && rm -rf /tmp/nomad.zip /tmp/nomad

ENTRYPOINT ["/usr/local/bin/nomad"]
