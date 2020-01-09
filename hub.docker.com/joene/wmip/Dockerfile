FROM alpine:latest
RUN apk add --no-cache curl iputils

RUN mkdir /health
COPY pingcheck.sh /health/
RUN chmod +x /health/pingcheck.sh

CMD while true; do curl -s ifconfig.co/ip; sleep 60; done
