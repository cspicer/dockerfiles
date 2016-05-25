FROM debian:latest
MAINTAINER Chris Spicer <git@cspicer.net>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -qq \
  && apt-get install -y \
    stow \
  && apt-get clean -y \
  && apt-get autoclean -y \
  && apt-get autoremove -y \
  && rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["stow"]
