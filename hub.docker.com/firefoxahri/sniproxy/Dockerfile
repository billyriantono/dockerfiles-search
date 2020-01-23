FROM alpine:latest

ENV UPSTREAM_DNS 8.8.8.8 8.8.4.4

RUN	apk update \
	&& apk add sniproxy

EXPOSE 443
ADD sniproxy.conf /sniproxy.conf

CMD ["sniproxy -f -c /sniproxy.conf"]