FROM alpine:3.11
MAINTAINER uc.dang@tiki.vn

# ENV
ENV LANG       en_US.UTF-8
ENV LC_ALL     en_US.UTF-8
ENV TZ         Asia/Saigon
ENV TIMEZONE Asia/Saigon
ENV TELEGRAF_VERSION 1.13.0

SHELL ["/bin/sh", "-c"]

# timezone and locale
RUN echo $TZ > /etc/timezone \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime

#install supervisor
RUN apk add --update supervisor && rm  -rf /tmp/* /var/cache/apk/*

#install fluentd
RUN apk update \
 && apk add --no-cache \
        ca-certificates \
        ruby ruby-irb ruby-etc ruby-webrick \
        tini \
 && apk add --no-cache --virtual .build-deps \
        build-base \
        ruby-dev gnupg \
 && echo 'gem: --no-document' >> /etc/gemrc \
 && gem install oj -v 2.18.3 \
 && gem install json -v 2.2.0 \
 && gem install fluentd -v 0.12.43 \
 && gem install bigdecimal -v 1.3.5 \
 && apk del .build-deps \
 && rm -rf /tmp/* /var/tmp/* /usr/lib/ruby/gems/*/cache/*.gem

#install telegraf
ADD https://dl.influxdata.com/telegraf/releases/telegraf-${TELEGRAF_VERSION}-static_linux_amd64.tar.gz ./
RUN tar -C . -xzf telegraf-${TELEGRAF_VERSION}-static_linux_amd64.tar.gz && \
        chmod +x telegraf/* && \
        cp telegraf/telegraf /usr/bin/ && \
        rm -rf *.tar.gz* telegraf/ 

# configuration
COPY conf/ /etc

# Start Supervisord
COPY ./start.sh /start.sh
RUN chmod 755 /start.sh

EXPOSE 24224 8125

CMD ["/bin/sh", "/start.sh"]
