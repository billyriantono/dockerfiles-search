FROM alpine:3.6

RUN set -ex; \
	mkdir /etc/ceilometer && \
	touch /etc/ceilometer/aaa /etc/ceilometer/bbb && \
	chown 18345:18345 -R /etc/ceilometer/ && \
	chmod 600 -R /etc/ceilometer/
