FROM alpine
RUN apk update && apk upgrade
RUN apk add tinyproxy curl

RUN chown nobody /var/run/tinyproxy

ADD tinyproxy.conf /etc/tinyproxy.conf

RUN touch /var/log/tinyproxy/tinyproxy.log && \
    chown nobody /var/log/tinyproxy/tinyproxy.log

ADD start.sh /
RUN chown nobody /start.sh && chmod +x /start.sh

EXPOSE 8888

ENTRYPOINT [ "/start.sh" ]
