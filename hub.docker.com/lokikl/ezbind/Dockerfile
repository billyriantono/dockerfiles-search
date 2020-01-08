FROM alpine:3.7

MAINTAINER dev@lokikl.com

RUN apk --update upgrade && \
    apk add --update bind ruby ruby-irb && \
    rm -rf /var/cache/apk/*

RUN mkdir -p /var/log/named /etc/bind

ADD init.sh /init.sh
ADD generate_bind_config.rb /generate_bind_config.rb
ADD named.conf /etc/bind/named.conf
RUN chmod 750 /init.sh

EXPOSE 53/udp

CMD ["/init.sh"]
