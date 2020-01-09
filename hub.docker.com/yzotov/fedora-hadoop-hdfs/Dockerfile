FROM yzotov/fedora-hadoop:2.7.1

MAINTAINER Yuriy Zotov <yura.zotov@gmail.com>

ADD core-site.xml /opt/hadoop/etc/hadoop/core-site.xml
ADD wait-hadoop.sh /opt/hadoop/sbin/wait-hadoop.sh
ADD run-hdfs.sh /run-hdfs.sh
ADD hdfs-site.xml /opt/hadoop/etc/hadoop/hdfs-site.xml

ENTRYPOINT ["/run-hdfs.sh"]
