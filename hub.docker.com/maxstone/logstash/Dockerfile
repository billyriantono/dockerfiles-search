FROM logstash
MAINTAINER rainer@nts.at

COPY logstash.conf /opt/logstash/config/
CMD ["-f", "/opt/logstash/config/logstash.conf"]

EXPOSE 5000 5000/udp
