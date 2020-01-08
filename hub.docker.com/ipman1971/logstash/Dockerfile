FROM ipman1971/java7_base
MAINTAINER ipman1971
 
ENV DEBIAN_FRONTEND noninteractive
 
RUN \
wget https://download.elastic.co/logstash/logstash/logstash-2.1.1.tar.gz && \
tar xvzf logstash-2.1.1.tar.gz && \
rm -f logstash-2.1.1.tar.gz && \
chown -R elkuser:elkuser logstash-2.1.1
 
# logstash.conf and Dockerfile must be on same location
ADD logstash.conf /home/elkuser
 
CMD logstash-2.1.1/bin/logstash -f logstash.conf --verbose
