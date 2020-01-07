FROM alpine:3.6
LABEL maintainer "Kyle Lucy <kmlucy@gmail.com>"

COPY ["cloudflare-update-record.sh","config.example","start.sh","/"]

RUN apk add --no-cache curl perl && \
	mkdir /config && \
	chmod +x /cloudflare-update-record.sh && \
	chmod +x /start.sh

WORKDIR /config

VOLUME /config

ENV RUN_AS_DAEMON=0 DAEMON_SLEEP_TIME=600
CMD ["/start.sh"]
