FROM rshinde26/cdh-hadoop-base

MAINTAINER Rahul Shinde <r.shinde2007@gmail.com>
LABEL description="Cloudera Hadoop 5.9 Namenode Docker Image"

RUN mkdir -p /hdfs/nm
RUN yum -y install hadoop-hdfs-namenode && rm -rf /var/cache/yum/*  && yum clean all
RUN hdfs namenode -format
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
EXPOSE 8020
VOLUME /hdfs
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
