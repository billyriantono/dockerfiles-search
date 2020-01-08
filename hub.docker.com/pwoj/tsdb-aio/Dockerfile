FROM pwoj/centos7:3

MAINTAINER Peter Wojciechowski <pwojciechowski@conversantmedia.com>

RUN cd /cnvr/sources && \
    curl -O http://mirror.jax.hugeserver.com/apache/zookeeper/zookeeper-3.4.10/zookeeper-3.4.10.tar.gz && \
    curl -O http://www.namesdir.com/mirrors/apache/hadoop/common/hadoop-2.8.1/hadoop-2.8.1.tar.gz && \
    curl -O http://apache.mirror.gtcomm.net/hbase/1.3.1/hbase-1.3.1-bin.tar.gz && \
    curl -L -O https://github.com/OpenTSDB/opentsdb/releases/download/v2.3.0/opentsdb-2.3.0.tar.gz && \
    tar -zxf zookeeper-3.4.10.tar.gz -C /cnvr/apps && \
    tar -zxf hadoop-2.8.1.tar.gz -C /cnvr/apps && \
    tar -zxf hbase-1.3.1-bin.tar.gz -C /cnvr/apps && \
    tar -zxf opentsdb-2.3.0.tar.gz -C /cnvr/sources && \
    mkdir -p /cnvr/data/hbase /cnvr/data/zookeeper /cnvr/data/tsdb /cnvr/data/hdfs && \
    mkdir -p /cnvr/logs/zookeeper /cnvr/logs/hadoop && \
    rm -rf /cnvr/apps/hbase-1.3.1/docs && \
    rm -rf /cnvr/apps/hadoop/share/doc && \
    rm -f /cnvr/apps/hbase-1.3.1/conf/hbase-site.xml && \
    rm -f /cnvr/sources/zookeeper-3.4.10.tar.gz && \
    rm -f /cnvr/sources/hadoop-2.8.1.tar.gz && \
    rm -f /cnvr/sources/hbase-1.3.1-bin.tar.gz && \
    rm -f /cnvr/sources/opentsdb-2.3.0.tar.gz && \
    ln -s /cnvr/apps/zookeeper-3.4.10 /cnvr/apps/zookeeper && \
    ln -s /cnvr/apps/hadoop-2.8.1 /cnvr/apps/hadoop && \
    ln -s /cnvr/apps/hbase-1.3.1 /cnvr/apps/hbase && \
    ln -s /cnvr/apps/opentsdb /cnvr/apps/tsdb && \
    yum install -y gcc make net-tools hostname && \
    cd /cnvr/sources/opentsdb-2.3.0 && \
    ./configure --prefix=/cnvr/apps/opentsdb && \
    make && make install && \
    rm -rf /cnvr/sources/opentsdb-2.3.0 && \
    yum autoremove -y make gcc && \
    yum autoremove -y && \
    yum clean all

COPY fs/runTsdb.sh /cnvr/
COPY fs/hbase/hbase-site.xml /cnvr/apps/hbase/conf/hbase-site.xml
COPY fs/opentsdb.conf /cnvr/apps/opentsdb/opentsdb.conf
COPY fs/zookeeper/zoo.cfg /cnvr/apps/zookeeper/conf/zoo.cfg
COPY fs/hadoop/core-site.xml /cnvr/apps/hadoop/etc/hadoop/core-site.xml
COPY fs/hadoop/hdfs-site.xml /cnvr/apps/hadoop/etc/hadoop/hdfs-site.xml

ENV ZOO_LOG_DIR=/cnvr/logs/zookeeper
ENV HADOOP_HOME=/cnvr/apps/hadoop
ENV HADOOP_LIBEXEC_DIR=/cnvr/apps/hadoop/libexec
ENV HADOOP_CONF_DIR=/cnvr/apps/hadoop/etc/hadoop
ENV HBASE_HOME=/cnvr/apps/hbase
ENV HBASE_CONF_DIR=/cnvr/apps/hbase/conf
ENV PATH=/cnvr/apps/zookeeper/bin:/cnvr/apps/hadoop/bin:/cnvr/apps/hbase/bin:/cnvr/apps/tsdb/bin:${PATH}

CMD ["/cnvr/runTsdb.sh"]

