FROM ipman1971/java7_base
MAINTAINER ipman1971
 
ENV DEBIAN_FRONTEND noninteractive
 
RUN \
wget https://download.elastic.co/kibana/kibana/kibana-4.3.1-linux-x64.tar.gz && \
tar xvzf kibana-4.3.1-linux-x64.tar.gz && \
rm -f kibana-4.3.1-linux-x64.tar.gz && \
chown -R elkuser:elkuser kibana-4.3.1-linux-x64
 
ADD kibana.yml kibana-4.3.1-linux-x64/config/kibana.yml
 
ENTRYPOINT kibana-4.3.1-linux-x64/bin/kibana
