FROM digitalwonderland/logstash-forwarder:latest

ADD logstash-forwarder.conf /opt/

ENTRYPOINT sleep 5; /var/lib/golang/bin/logstash-forwarder -config /opt/logstash-forwarder.conf
