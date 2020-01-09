FROM alpine:3.6

MAINTAINER  Thiago Figueiro <thiagocsf@gmail.com>

ENV BACKEND_HOST localhost
ENV BACKEND_PORT 80
ENV VARNISH_SERVICE_PORT 6081
ENV VARNISH_MEMORY 128M

EXPOSE 6081

RUN apk add --no-cache --virtual .secret-deps \
      curl \
    && apk --no-cache add \
      varnish

RUN curl -s https://configs-devops-mobydigital.netlify.com/magento2/varnish/start.sh > /start.sh \
    && chmod +x /start.sh \
    && mkdir -p /etc/varnish \
    && curl -s https://configs-devops-mobydigital.netlify.com/magento2/varnish/default.vcl > /etc/varnish/default.vcl \
    && apk del --no-cache .secret-deps \
    rm -rf /var/cache/apk/* /root/.cache

ENTRYPOINT ["/start.sh"]
