FROM alpine:3.3

ENV LUA_VERSION 5.1.5
ENV LUA_URL http://www.lua.org/ftp/lua-${LUA_VERSION}.tar.gz
ENV LUAROCKS_VERSION 2.3.0
ENV LUAROCKS_URL http://luarocks.org/releases/luarocks-${LUAROCKS_VERSION}.tar.gz

RUN apk add --no-cache \
    curl \
    zip \
    unzip \
    readline \
    ncurses-libs \
  && apk add --no-cache --virtual \
    build-deps \
    gcc \
    musl-dev \
    readline-dev \
    ncurses-dev \
    make \
  && curl -sSL ${LUA_URL} | tar -zxC /tmp \
  && cd /tmp/lua-${LUA_VERSION} \
  && make linux install \
  && curl -sSL ${LUAROCKS_URL} | tar -zxC /tmp \
  && cd /tmp/luarocks-${LUAROCKS_VERSION} \
  && ./configure \
  && make bootstrap \
  && luarocks install moonscript \
  && apk del build-deps \
  && rm -rf /tmp/lua-* \
  && rm -rf /tmp/luarocks-*
