FROM alpine:latest
MAINTAINER Chris Spicer <github@cspicer.ca>

RUN apk add --update \
    git \
    build-base \
    cmake \
    libpng-dev \
    libjpeg-turbo-dev \
    boost-dev \
    boost-iostreams \
    boost-system \
    boost-filesystem \
    boost-program_options \
  && rm -rf /var/cache/apk/*

RUN git clone --depth 1 \
    https://github.com/mapcrafter/mapcrafter.git \
    /tmp/mapcrafter \
  && cd /tmp/mapcrafter \
  && cmake . \
  && make install \
  && rm -rf /tmp/mapcrafter

ENTRYPOINT ["mapcrafter"]
CMD ["--help"]
