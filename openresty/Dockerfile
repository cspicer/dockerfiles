FROM cspicer/lua:5.1

ENV OPENRESTY_VERSION 1.9.7.3
ENV OPENRESTY_ARCHIVE_URL http://openresty.org/download/openresty-${OPENRESTY_VERSION}.tar.gz

ENV OPENRESTY_PREFIX /opt/openresty
ENV NGINX_PREFIX /opt/openresty/nginx
ENV VAR_PREFIX /var/nginx

ENV SOURCE_DIR /usr/local/src

RUN apk add --no-cache \
    curl \
    libpcrecpp \
    libpcre16 \
    libpcre32 \
    openssl \
    libssl1.0 \
    pcre \ 
    libgcc \
    libstdc++

RUN apk add --no-cache --virtual build-deps \
    tar \
    make \
    gcc \
    musl-dev \
    pcre-dev \
    openssl-dev \
    zlib-dev \
    ncurses-dev \
    readline-dev \
    perl \
  && curl \
    --silent \
    --show-error \
    --create-dirs \
    --location ${OPENRESTY_ARCHIVE_URL} \
    --output /tmp/openresty.tar.gz \
  && mkdir -p ${SOURCE_DIR} \
  && tar -C ${SOURCE_DIR} -zxf /tmp/openresty.tar.gz \
  && cd ${SOURCE_DIR}/openresty-${OPENRESTY_VERSION} \
  && readonly BUILDERS=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
  && ./configure \
    --prefix=$OPENRESTY_PREFIX \
    --http-client-body-temp-path=$VAR_PREFIX/client_body_temp \
    --http-proxy-temp-path=$VAR_PREFIX/proxy_temp \
    --http-log-path=$VAR_PREFIX/access.log \
    --error-log-path=$VAR_PREFIX/error.log \
    --pid-path=$VAR_PREFIX/nginx.pid \
    --lock-path=$VAR_PREFIX/nginx.lock \
    --with-luajit \
    --with-pcre-jit \
    --with-ipv6 \
    --with-http_ssl_module \
    --without-http_ssi_module \
    --without-http_userid_module \
    --without-http_fastcgi_module \
    --without-http_uwsgi_module \
    --without-http_scgi_module \
    --without-http_memcached_module \
    -j${BUILDERS} \
  && make -j${BUILDERS} \
  && make install \
  && apk del build-deps \
  && rm -rf /tmp/openresty*

RUN ln -sf $NGINX_PREFIX/sbin/nginx /usr/local/bin/nginx \
  && ln -sf $NGINX_PREFIX/sbin/nginx /usr/local/bin/openresty \
  && ln -sf $OPENRESTY_PREFIX/bin/resty /usr/local/bin/resty \
  && ln -sf $OPENRESTY_PREFIX/luajit/bin/luajit-* $OPENRESTY_PREFIX/luajit/bin/lua \
  && ln -sf $OPENRESTY_PREFIX/luajit/bin/luajit-* /usr/local/bin/lua

WORKDIR $NGINX_PREFIX
ENTRYPOINT ["nginx"]
CMD ["-g", "daemon off; error_log /dev/stderr info;"]

