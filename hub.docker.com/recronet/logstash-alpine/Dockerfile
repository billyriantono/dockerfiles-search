FROM alpine:3.2
MAINTAINER davor.serfez@recro-net.hr
RUN apk add --update openjdk7-jre-base openssl bash && \
  wget -O /tmp/logstash-1.5.3.tar.gz https://download.elastic.co/logstash/logstash/logstash-1.5.3.tar.gz && \
  wget -O /usr/bin/etcdctl http://serfez.net/etcdctl && \
  chmod +x /usr/bin/etcdctl && \
  mkdir /opt && \
  tar xzf /tmp/logstash-1.5.3.tar.gz -C /opt/ && \
  mv /opt/logstash-1.5.3 /opt/logstash && \
  rm -Rf /var/cache/apk/* /tmp/*

ADD cacert.pem /opt/logstash/cacert.pem

ENV SSL_CERT_FILE /opt/logstash/cacert.pem

WORKDIR /opt/logstash

#ADD store.jks /opt/logstash/store.jks
#ADD /opt/boot.sh


#CMD /opt/boot.sh

#-Djavax.net.ssl.trustStore=/opt/logstash/store.jks
#-Djavax.net.ssl.trustStore=samplecacerts
#export SSL_CERT_FILE=/opt/logstash/cacert.pem 
#ca-certificates 