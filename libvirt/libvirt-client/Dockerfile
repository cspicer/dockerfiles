FROM debian:jessie
MAINTAINER Chris Spicer <git@cspicer.net>

ENV DEBIAN_FRONTEND noninteractive

ENV APP_NAME virt-manager
ENV APP_VERSION 1.2.1
ENV ARCHIVE_URL https://fedorahosted.org/released/${APP_NAME}/${APP_NAME}-${APP_VERSION}.tar.gz

RUN apt-get update -qq \
  && apt-get install -y \
    curl \
    libvirt-clients \
    libglib2.0-bin \
    python-gi \
    python-ipaddr \
    python-urlgrabber \
    python-libxml2 \
    libosinfo-1.0-dev \
    intltool \
  && apt-get install -y --no-install-recommends \
    python-libvirt

RUN curl -sSL ${ARCHIVE_URL} -o /tmp/${APP_NAME}-${APP_VERSION}.tar.gz \
  && tar -zxf /tmp/${APP_NAME}-${APP_VERSION}.tar.gz -C /tmp \
  && cd /tmp/${APP_NAME}-${APP_VERSION} \
  && python setup.py install --prefix=/usr \
  && rm -rf /tmp/${APP_NAME}-${APP_VERSION}.tar.gz /tmp/${APP_NAME}-${APP_VERSION}

VOLUME [ "/var/lib/libvirt/" ]

CMD ["/usr/bin/virsh"]
