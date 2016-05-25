FROM alpine:latest
MAINTAINER Chris Spicer <git@cspicer.net>

ENV ANSIBLE_VERSION 2.0.1.0

RUN apk add --update \
    build-base \
    bash \
    openssh-client \
    python \
    python-dev \
    py-pip \ 
    git \
  && pip install --upgrade pip \
  && pip install \
    http://releases.ansible.com/ansible/ansible-${ANSIBLE_VERSION}.tar.gz \
    awscli \
    requests \
    docker-py \
    boto \
    dopy \
    dnsimple
 
RUN rm -rf /var/cache/apk/*

ENTRYPOINT ["ansible"]
CMD ["--help"]
