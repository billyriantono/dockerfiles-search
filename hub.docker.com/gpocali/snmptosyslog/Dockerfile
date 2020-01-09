FROM alpine:latest

RUN sed -i -e "s/#//" /etc/apk/repositories && \
	apk update && \
	apk add --no-cache net-snmp syslog-ng

RUN mkdir -p /etc/snmptrapd/mibs/
COPY ./syslog-ng.conf /etc/syslog-ng/syslog-ng.conf
COPY ./snmptrapd.conf /etc/snmptrapd/snmptrapd.conf
COPY ./trapLaunch /bin/trapLaunch
RUN chmod +x /bin/trapLaunch
WORKDIR /var/log/

EXPOSE 162/udp

CMD ["/bin/trapLaunch"]
