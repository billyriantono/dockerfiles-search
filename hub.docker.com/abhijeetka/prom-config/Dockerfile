
FROM alpine
MAINTAINER Abhijeet Kamble (abhijeet.kamble619@gmail.com)

RUN mkdir -p /etc/prom-conf/

ADD prometheus.yml /etc/prom-conf/prometheus.yml
ADD alert.rules /etc/prom-conf/alert.rules

CMD ["/bin/sh"]
