FROM smatochkin/elasticsearch:1.3.4

# Install Logstash binaries
RUN curl -Ls https://download.elasticsearch.org/logstash/logstash/logstash-1.4.2.tar.gz | \
    tar xz -C /opt && \
    ln -s logstash-1.4.2 /opt/logstash

# Upload Logstash configuration and startup files
RUN mkdir /etc/service/logstash
ADD config/logstash.conf /opt/logstash/config/logstash.conf
ADD service /etc/service

# Expose communication ports
EXPOSE 5000 5000/udp
