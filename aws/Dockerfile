FROM alpine:latest
MAINTAINER Chris Spicer <git@cspicer.net>

ENV AWS_CLI_VERSION 1.10.26

RUN apk add --no-cache \
    python \
    py-pip \ 
  && pip install --upgrade pip \
  && pip install \
    boto3 \
    awscli==${AWS_CLI_VERSION} \
    aws-shell

ENTRYPOINT ["/usr/bin/aws"]
