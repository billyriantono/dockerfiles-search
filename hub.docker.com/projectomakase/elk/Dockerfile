FROM willdurand/elk:latest

MAINTAINER Richard Lucas <feedback@projectomakase.org>

COPY etc/logstash/logstash-wildfly.conf /etc/logstash/logstash-wildfly.conf

EXPOSE 80 5043

CMD [ "/usr/bin/supervisord", "-n", "-c", "/etc/supervisor/supervisord.conf" ]