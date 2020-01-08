FROM logstash:2.1.1
MAINTAINER tldr

COPY files/conf/ /conf

EXPOSE 5000
EXPOSE 5000/udp

CMD [ "-f", "/conf" ]