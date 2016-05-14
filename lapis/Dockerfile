FROM cspicer/openresty:1.9.7.3

ENV LAPIS_OPENRESTY "/opt/openresty/nginx/sbin/nginx"
ENV LAPIS_ENVIRONMENT "development"

RUN apk add --no-cache --virtual build-deps \
    git \
    gcc \
    musl-dev \
    openssl-dev \
    libssl1.0 \
  && luarocks install lapis \
  && apk del build-deps

CMD ["/usr/local/bin/lapis", "server", "$LAPIS_ENVIRONMENT"]

