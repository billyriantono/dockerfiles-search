FROM centos
RUN yum install -y https://github.com/kairosdb/kairosdb/releases/download/v1.1.1/kairosdb-1.1.1-1.rpm https://github.com/kairosdb/kairos-carbon/releases/download/v1.0-1/kairos-carbon-1.0-1.rpm
COPY files/opt/kairosdb/conf/kairosdb.properties /opt/kairosdb/conf/kairosdb.properties
WORKDIR /opt/kairosdb/bin

EXPOSE 8080 4242 2003 

CMD /opt/kairosdb/bin/kairosdb.sh run
