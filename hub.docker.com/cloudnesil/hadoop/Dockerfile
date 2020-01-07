# Creates pseudo distributed hadoop 2.7.1
#
# docker build -t cloudnesil/hadoop .

FROM cloudnesil/hadoop:master

USER root


# distributed
ADD core-site.xml.template $HADOOP_PREFIX/etc/hadoop/core-site.xml.template

ADD hdfs-site.xml $HADOOP_PREFIX/etc/hadoop/hdfs-site.xml

ADD mapred-site.xml $HADOOP_PREFIX/etc/hadoop/mapred-site.xml

ADD yarn-site.xml $HADOOP_PREFIX/etc/hadoop/yarn-site.xml



ADD bootstrap.sh /etc/bootstrap.sh
RUN chown root:root /etc/bootstrap.sh
RUN chmod 700 /etc/bootstrap.sh

ENV BOOTSTRAP /etc/bootstrap.sh




CMD ["/etc/bootstrap.sh", "-d"]

# Hdfs ports
EXPOSE 50010 50020 50070 50075 50090 8020 9000
# Mapred ports
EXPOSE 19888
#Yarn ports
EXPOSE 8030 8031 8032 8033 8040 8042 8088
#Other ports
EXPOSE 49707 2122