FROM alpine:latest
MAINTAINER atomney <atomney+docker@gmail.com>
ADD start-catproxy.sh /start-catproxy.sh
ADD privoxy.conf /etc/privoxy/config
ADD user.filter /etc/privoxy/user.filter
ADD user.action /etc/privoxy/user.action
RUN apk add --no-cache privoxy darkhttpd && \
        chown -R privoxy /etc/privoxy && \
        chmod +x /start-catproxy.sh && \
	mkdir -p /www

ADD cat1.png /www/.

USER privoxy
EXPOSE 8118 8080
CMD ["/start-catproxy.sh"]
