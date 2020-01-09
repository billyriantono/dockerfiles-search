FROM hasholding/alpine-base:3.8
LABEL maintainer "Levent SAGIROGLU <LSagiroglu@gmail.com>"

EXPOSE 80 443
ENV WEB_CONF "/etc/nginx/conf.d/default.conf"
VOLUME /shared

RUN apk add --update --no-cache nginx && \
    mkdir -p /run/nginx

COPY entrypoint.sh /bin/entrypoint.sh
COPY default.conf /etc/nginx/conf.d/default.conf
ENTRYPOINT ["/bin/entrypoint.sh"]
