FROM cspicer/qemu:latest
MAINTAINER Chris Spicer <git@cspicer.net>

ENV DEBIAN_FRONTEND noninteractive

ENV APP_NAME libvirt
ENV APP_VERSION 1.2.21
ENV ARCHIVE_URL http://libvirt.org/sources/${APP_NAME}-${APP_VERSION}.tar.gz

RUN apt-get update -qq \
  && apt-get install -y \
    curl \
    build-essential \
    pkg-config \
    libxml2-dev \
    libdevmapper-dev \
    libyajl-dev \
    libnl-3-dev \
    libnl-route-3-dev \
    python-dev

RUN curl -sSL ${ARCHIVE_URL} -o /tmp/${APP_NAME}-${APP_VERSION}.tar.gz \
  && tar -zxf /tmp/${APP_NAME}-${APP_VERSION}.tar.gz -C /tmp \
  && cd /tmp/${APP_NAME}-${APP_VERSION} \
  && ./configure --prefix=/usr --localstatedir=/var --sysconfdir=/etc \
  && make install \
  && rm -rf /tmp/${APP_NAME}-${APP_VERSION}.tar.gz /tmp/${APP_NAME}-${APP_VERSION}

RUN mkdir -p /etc/libvirt/qemu/ \
  && echo "listen_tls = 0" >> /etc/libvirt/libvirtd.conf \
  && echo 'listen_tcp = 1' >> /etc/libvirt/libvirtd.conf \
  && echo 'tls_port = "16514"' >> /etc/libvirt/libvirtd.conf \
  && echo 'tcp_port = "16509"' >> /etc/libvirt/libvirtd.conf \
  && echo 'auth_tcp = "none"' >> /etc/libvirt/libvirtd.conf \
  && echo 'user = "root"' >> /etc/libvirt/qemu.conf

VOLUME [ "/sys/fs/cgroup" ]
VOLUME [ "/var/lib/libvirt/" ]

CMD ["/usr/bin/virsh"]
