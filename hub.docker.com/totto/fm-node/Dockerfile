#
# Apache Synapse 2.1.0
#
FROM azul/zulu-openjdk:8
MAINTAINER Totto (totto@totto.org)

RUN apt-get -qq update \
    && apt-get -yqq install ca-certificates ssl-cert wget



# copy zip from local folder to container
RUN wget -P /opt http://apache.mirrors.lucidnetworks.net//synapse/2.1.0/synapse-2.1.0-bin.tar.gz && \
    apt-get update && \
    apt-get install -y zip && \
    apt-get clean  
#RUN apt-get install -y gz
RUN cd /opt && gzip -d synapse-2.1.0-bin.tar.gz 
RUN cd /opt && tar xvf synapse-2.1.0-bin.tar 
#    rm /opt/synapse-2.1.0-bin.tar.gz
RUN wget -P /opt/synapse-2.1.0/lib http://central.maven.org/maven2/org/apache/axis2/axis2-transport-tcp/1.0.0/axis2-transport-tcp-1.0.0.jar

ADD synapse.xml  /opt/synapse-2.1.0/repository/conf/synapse-config/synapse.xml  
ADD axis2-tcptransport.xml /opt/synapse-2.1.0/repository/conf/axis2.xml

ENV JAVA_HOME /usr/lib/jvm/zulu-8-amd64
EXPOSE 9443 6060 

CMD ["/opt/synapse-2.1.0/bin/synapse.sh"]
