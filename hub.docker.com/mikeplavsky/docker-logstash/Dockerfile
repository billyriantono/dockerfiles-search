FROM dockerfile/java:oracle-java7

ENV LS_PKG_NAME logstash-1.4.2

# Install LogStash.
RUN \
  cd / && \
  wget https://download.elasticsearch.org/logstash/logstash/$LS_PKG_NAME.tar.gz && \
  tar xvzf $LS_PKG_NAME.tar.gz && \
  rm -f $LS_PKG_NAME.tar.gz && \
  mv /$LS_PKG_NAME /logstash
