FROM mini/base

# Build from mini/base, get updates and upgrade, add bash, then install Caddy
RUN apk update && apk upgrade && apk add bash && \
    curl -fsSL https://getcaddy.com | bash -s personal http.cors,http.ipfilter,http.proxyprotocol,http.ratelimit,http.realip && \
    /usr/local/bin/caddy -version

EXPOSE 80 443
VOLUME /root/.caddy
WORKDIR /srv

ENTRYPOINT ["/usr/local/bin/caddy"]
# Added `-agree` flag to preapprove Let's Encrypt legalese
CMD ["--conf", "/etc/Caddyfile", "--log", "stdout", "-agree"]
