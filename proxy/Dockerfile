FROM mini/base

RUN apk update && apk upgrade && apk add bash && \
    curl -fsSL https://getcaddy.com | bash -s personal http.cors,http.ipfilter,http.proxyprotocol,http.ratelimit,http.realip && \
    /usr/local/bin/caddy -version

EXPOSE 80 443
VOLUME /root/.caddy
WORKDIR /srv

ENTRYPOINT ["/usr/local/bin/caddy"]
CMD ["--conf", "/etc/Caddyfile", "--log", "stdout", "-agree"]
