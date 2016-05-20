FROM alpine:latest
MAINTAINER Chris Spicer <github@cspicer.ca>

ENV TERRAFORM_VERSION 0.6.15
ENV TERRAFORM_RELEASE_URL https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip
ENV GLIBC_VERSION 2.23-r1
ENV GLIBC_RELEASE_URL https://github.com/andyshinn/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}
ENV GLIBC_KEY_URL https://raw.githubusercontent.com/andyshinn/alpine-pkg-glibc/master/andyshinn.rsa.pub
ENV GLIBC_KEY_PATH /etc/apk/keys/andyshinn.rsa.pub

RUN apk add --no-cache \
    ca-certificates \
    curl \
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
  --location "${TERRAFORM_RELEASE_URL}" \
  --output /tmp/terraform_${TERRAFORM_VERSION}.zip \
  && unzip /tmp/terraform_${TERRAFORM_VERSION}.zip -d /tmp/terraform \
  && cp -R /tmp/terraform/* /usr/local/bin \
  && rm -rf /tmp/terraform_${TERRAFORM_VERSION}.zip /tmp/terraform

ENTRYPOINT ["/usr/local/bin/terraform"]

