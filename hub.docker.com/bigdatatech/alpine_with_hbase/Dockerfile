FROM bigdatatech/alpine_with_jdk8


MAINTAINER sandeep <bigdatatechcomputing@gmail.com>

RUN mkdir /hbase

RUN wget -q -P /tmp http://www-eu.apache.org/dist/hbase/stable/hbase-1.2.4-bin.tar.gz 

RUN tar xzvf /tmp/hbase-1.2.4-bin.tar.gz -C /hbase && mv /hbase/hbase-1.2.4/* /hbase && rm -rf /tmp/hbase-1.2.4-bin.tar.gz

RUN sed -i -e "s/# export JAVA_HOME=\/usr\/java\/jdk1.6.0\//export JAVA_HOME=\/usr\/lib\/jvm\/java-1.8-openjdk/g" /hbase/conf/hbase-env.sh

RUN echo "<configuration>" > /hbase/conf/hbase-site.xml
RUN echo "  <property>" >> /hbase/conf/hbase-site.xml
RUN echo "    <name>hbase.rootdir</name>" >> /hbase/conf/hbase-site.xml
RUN echo "    <value>file:///hbase/hbase_root</value>" >> /hbase/conf/hbase-site.xml
RUN echo "  </property>" >> /hbase/conf/hbase-site.xml
RUN echo "  <property>" >> /hbase/conf/hbase-site.xml
RUN echo "    <name>hbase.zookeeper.property.dataDir</name>" >> /hbase/conf/hbase-site.xml
RUN echo "    <value>/hbase/zookeeper</value>" >> /hbase/conf/hbase-site.xml
RUN echo "  </property>" >> /hbase/conf/hbase-site.xml
RUN echo "</configuration>" >> /hbase/conf/hbase-site.xml

RUN apk update && apk add git

CMD /hbase/bin/hbase master start
