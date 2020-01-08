FROM nginx:1.15.9-alpine

LABEL maintainer "Yeray Medina López <ymedlop@gmail.com>"

# TODO: Get by URL from a environment variable.
ADD oauth2_proxy/oauth2_proxy /usr/local/bin/oauth2_proxy
ADD oauth2_proxy/oauth2_proxy.cfg /etc/oauth2_proxy.cfg

ADD conf.d/default.conf /etc/nginx/conf.d/default.conf
ADD services/oauth2_proxyd /etc/init.d/oauth2_proxyd

RUN addgroup -S oauth2_proxy
RUN adduser -S -D oauth2_proxy oauth2_proxy

RUN chown -R oauth2_proxy:oauth2_proxy /usr/local/bin/oauth2_proxy
RUN chmod +x /usr/local/bin/oauth2_proxy
RUN chmod +x /etc/init.d/oauth2_proxyd

EXPOSE 8080

CMD ["/etc/init.d/oauth2_proxyd"]
