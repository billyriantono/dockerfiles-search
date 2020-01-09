FROM java:7-jre

ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64/jre

RUN wget --quiet -O - http://www.us.apache.org/dist/hbase/hbase-0.98.12/hbase-0.98.12-hadoop2-bin.tar.gz | tar --directory /usr/local -xzf -
RUN ln -s /usr/local/hbase-0.98.12-hadoop2 /usr/local/hbase

ADD start.sh /usr/local/hbase/start-tail.sh
ADD hbase-site.xml /usr/local/hbase/conf/

RUN sed -i.bak -r 's/=(INFO|DEBUG)/=WARN/' /usr/local/hbase/conf/log4j.properties

VOLUME ["/var/lib/hbase", "/var/lib/zookeeper"]
EXPOSE 2181 60000 60020

CMD /usr/local/hbase/start-tail.sh
