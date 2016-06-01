FROM debian:jessie

ENV NETATALK_VERSION 3.1.8
ENV NETATALK_SRC_URL http://ufpr.dl.sourceforge.net/project/netatalk/netatalk/${NETATALK_VERSION}/netatalk-${NETATALK_VERSION}.tar.gz

RUN apt-get update -qq \
  && apt-get install \
    --no-install-recommends \
    --fix-missing \
    --assume-yes \
    curl

WORKDIR /usr/local/src

RUN apt-get install -y --no-install-recommends \
    build-essential \
    libevent-dev \
    libssl-dev \
    libgcrypt11-dev \
    libkrb5-dev \
    libpam0g-dev \
    libwrap0-dev \
    libdb-dev \
    libtdb-dev \
    libmysqlclient-dev \
    libavahi-client-dev \
    libacl1-dev \
    libldap2-dev \
    libcrack2-dev \
    systemtap-sdt-dev \
    libdbus-1-dev \
    libdbus-glib-1-dev \
    libglib2.0-dev \
    libtracker-sparql-1.0-dev \
    libtracker-miner-1.0-dev \
  && curl \
    --silent \
    --show-error \
    --location ${NETATALK_SRC_URL} | tar zxv \
  && cd /usr/local/src/netatalk-${NETATALK_VERSION} \
  && ./configure \
    --with-init-style=debian-systemd \
    --with-zeroconf \
    --with-cracklib \
    --with-pam-confdir=/etc/pam.d \
    --with-dbus-sysconf-dir=/etc/dbus-1/system.d \
  && make \
  && make install \
  && mkdir /srv/backup \
  && cd /srv/backup \
  && rm -rf /usr/local/src/netatalk-${NETATALK_VERSION} \
  && apt-get purge --quiet --yes --auto-remove \
      build-essential \
      libevent-dev \
      libssl-dev \
      libgcrypt11-dev \
      libkrb5-dev \
      libpam0g-dev \
      libwrap0-dev \
      libdb-dev \
      libtdb-dev \
      libmysqlclient-dev \
      libavahi-client-dev \
      libacl1-dev \
      libldap2-dev \
      libcrack2-dev \
      systemtap-sdt-dev \
      libdbus-1-dev \
      libdbus-glib-1-dev \
      libglib2.0-dev \
      libtracker-sparql-1.0-dev \
      libtracker-miner-1.0-dev \
      tracker-gui \ 
      libgl1-mesa-dri \
  && apt-get install --yes \
      libevent-2.0 \
      libavahi-client3 \
      libevent-core-2.0 \
      libwrap0 \
      libtdb1 \
      libmysqlclient18 \
      libcrack2 \
      libdbus-glib-1-2 \
  && apt-get clean --yes \
  && apt-get autoclean --yes \
  && apt-get autoremove --yes \
  && rm -rf /var/lib/apt/lists/* 

WORKDIR /srv/backup
