FROM logstash:2.3.2

COPY ./template.json /template.json
COPY ./logstash.conf /logstash.conf

EXPOSE 5505/tcp
EXPOSE 5505/udp

CMD logstash -f /logstash.conf
