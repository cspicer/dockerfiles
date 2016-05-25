FROM debian:jessie
MAINTAINER Chris Spicer <git@cspicer.net>

ENV APP_NAME qemu
ENV APP_VERSION 2.4.1
ENV ARCHIVE_URL http://wiki.qemu-project.org/download/${APP_NAME}-${APP_VERSION}.tar.bz2
ENV VFIO_SCRIPT_URL https://gist.githubusercontent.com/cspicer/ff78616c98fe68965bbf/raw/55cda9406c3d03fda8e15efb9835b42386679579/vfio-bind
    
RUN sed -i 's/jessie main/jessie main non-free/' /etc/apt/sources.list \
  && apt-get update -qq \
  && apt-get install -y  \
    curl \
    build-essential \
    libusb-1.0-0-dev \
    pkg-config \
    zlib1g-dev \
    libglib2.0-dev \
    libpixman-1-dev \
  && curl -sSL ${ARCHIVE_URL} -o /tmp/${APP_NAME}-${APP_VERSION}.tar.bz2 \
  && tar -xjf /tmp/${APP_NAME}-${APP_VERSION}.tar.bz2 -C /tmp \
  && cd /tmp/${APP_NAME}-${APP_VERSION} \
  && ./configure --target-list=x86_64-softmmu --enable-libusb \
  && make -j8 clean \
  && make install \
  && rm -rf /tmp/${APP_NAME}* \
  && apt-get remove -y --purge \
    build-essential \
    zlib1g-dev \
  && apt-get clean -y \
  && apt-get autoclean -y \
  && apt-get autoremove -y

RUN mkdir -p /usr/share/ovmf/ \
  && curl -sSL ${VFIO_SCRIPT_URL} -o /usr/local/bin/vfio-bind \
  && chmod 755 /usr/local/bin/vfio-bind

COPY ovmf-code.fd /usr/share/ovmf/
COPY ovmf-vars.fd /usr/share/ovmf/
COPY ovmf-efi.fd /usr/share/ovmf/
