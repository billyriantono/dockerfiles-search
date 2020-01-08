FROM alpine

LABEL maintainer="Franck Coutouly <towl.fr@gmail.com>"

RUN apk add --update --no-cache varnish pwgen

RUN pwgen 50 1 > /etc/varnish/secret

COPY conf/drupal.vcl /etc/varnish/

ENTRYPOINT ["varnishd"]

CMD ["-F", "-a", ":80", "-f", "/etc/varnish/drupal.vcl", "-S", "/etc/varnish/secret", "-s", "malloc,1024m"]
