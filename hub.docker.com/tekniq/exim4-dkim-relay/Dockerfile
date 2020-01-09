FROM alpine:3.7
MAINTAINER Tyler Griesbach <tgriesbach@tekniq.com>

ENV RELAY_FROM_HOSTS=172.16.0.0/12 \
    DKIM_KEY_SIZE=1024 \
    DKIM_SELECTOR=dkim \
    DKIM_SIGN_HEADERS=Date:From:To:Subject:Message-ID

RUN apk --no-cache add exim libcap openssl \
    && mkdir /dkim /var/spool/exim \
    && chown -R exim: /dkim /var/log/exim /usr/lib/exim /var/spool/exim \
    && chmod 0755 /usr/sbin/exim \
    && setcap cap_net_bind_service=+ep /usr/sbin/exim \
    && apk del libcap

COPY ./entrypoint.sh /
COPY ./exim.conf /etc/exim

USER exim
VOLUME ["/dkim"]
EXPOSE 25

ENTRYPOINT ["/entrypoint.sh"]
CMD ["-bdf", "-q15m"]