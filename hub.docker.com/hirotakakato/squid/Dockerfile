FROM alpine:latest

RUN set -eux; \
    apk add --no-cache iptables squid thttpd; \
    sed /etc/squid/squid.conf \
      -e '/^#http_access deny to_localhost$/ s/^#//' \
      -e '/^http_port 3128$/ a http_port 3129 intercept' \
      -e '/^#cache_dir / s/^#//' \
      -e '/^cache_dir / s/ 100 / 10000 /' \
      -e '/^cache_dir / a maximum_object_size 5 GB' \
      -e '$ a \\n' \
      -e '$ a access_log stdio:/dev/stdout combined' \
      -e '$ a cache_log /dev/stderr' \
      -e '$ a forwarded_for delete' \
      -e '$ a shutdown_lifetime 1 second' \
      -e '$ a visible_hostname squid' \
      -e '$ a \\n' \
      -e '$ a acl url_rewrite url_regex ^http://mirrorlist\.centos\.org/?' \
      -e '$ a \\n' \
      -e '$ a url_rewrite_access allow url_rewrite' \
      -e '$ a url_rewrite_children 1 startup=1' \
      -e '$ a url_rewrite_program /etc/squid/url_rewrite' \
      -i; \
    echo -e '#!/bin/sh\nwhile read url trash; do echo "$url" | sed "s|^http://mirrorlist\.centos\.org/?release=\([^&]\+\)&arch=\([^&]\+\)&repo=\([^&]\+\).*$|http://127.0.0.1:3127/?${CENTOS_MIRROR_URL:-http://ftp.iij.ad.jp/pub/linux/centos/}\\1/\\3/\\2/|"; done' \
      | install -m 755 /dev/stdin /etc/squid/url_rewrite; \
    echo -e '#!/bin/sh\necho "Content-type: text/plain\n\n$QUERY_STRING"' \
      | install -m 755 /dev/stdin /var/www/http/index.cgi; \
    chown squid: /dev/stderr; \
    squid -Nz

VOLUME ["/var/cache/squid"]

COPY cmd.sh /

CMD ["/cmd.sh"]
