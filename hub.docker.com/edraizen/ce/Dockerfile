FROM java:8-jdk

# install necessary dependencies
RUN apt-get update && \
    apt-get install -y wget

WORKDIR /opt
RUN wget -O ce.tgz http://source.rcsb.org/download/protein-comparison-tool_20150211.tar.gz
RUN tar -xzf ce.tgz
RUN rm ce.tgz
RUN chmod +x /opt/biojava-protein-comparison-tool-4.0.0/runCE.sh

COPY wrapper.sh /opt/biojava-protein-comparison-tool-4.0.0

RUN mkdir /data
WORKDIR /data

ENTRYPOINT ["sh", "/opt/biojava-protein-comparison-tool-4.0.0/wrapper.sh"]
