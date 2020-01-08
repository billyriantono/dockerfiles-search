FROM centos:7
MAINTAINER Frank Fuhrmann <frank.fuhrmann@mailbox.org>

ENV PATH=/bin:/usr/bin:/usr/local/bin:/sbin:/usr/sbin:/usr/local/sbin

# update system
RUN yum -y update

# create some directories we need
RUN mkdir /data

RUN mkdir /data/elasticsearch
RUN mkdir /data/elasticsearch/data
RUN mkdir /data/elasticsearch/logs

RUN yum -y install epel-release
RUN yum -y update

RUN yum -y install wget
	
# install java
RUN cd /usr/src && wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u144-b01/090f390dda5b47b9b721c7dfaa008135/jdk-8u144-linux-x64.rpm"
RUN cd /usr/src && yum -y localinstall jdk-8u144-linux-x64.rpm

# prepare package installation
RUN rpm --import http://packages.elastic.co/GPG-KEY-elasticsearch

COPY conf/yum/elasticsearch.repo /etc/yum.repos.d/elasticsearch.repo

RUN yum -y install elasticsearch

RUN chown -R elasticsearch:elasticsearch /data/elasticsearch
COPY conf/elasticsearch/elasticsearch.yml /etc/elasticsearch/elasticsearch.yml
RUN rm -rf /var/lib/elasticsearch
RUN ln -s /data/elasticsearch/data /var/lib/elasticsearch
RUN rm -rf /var/log/elasticsearch
RUN ln -s /data/elasticsearch/logs /var/log/elasticsearch

RUN usermod -s /bin/bash elasticsearch

RUN yum -y remove wget
RUN yum -y clean all
RUN rm /usr/src/jdk-8u144-linux-x64.rpm

EXPOSE 9200
EXPOSE 9300
VOLUME /data/elasticsearch/data
VOLUME /data/elasticsearch/logs

CMD sh -c 'su elasticsearch -c "/bin/java -Xms2g -Xmx2g -XX:+UseConcMarkSweepGC -XX:CMSInitiatingOccupancyFraction=75 -XX:+UseCMSInitiatingOccupancyOnly -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -server -Xss1m -Djava.awt.headless=true -Dfile.encoding=UTF-8 -Djna.nosys=true -Djdk.io.permissionsUseCanonicalPath=true -Dio.netty.noUnsafe=true -Dio.netty.noKeySetOptimization=true -Dlog4j.shutdownHookEnabled=false -Dlog4j2.disable.jmx=true -Dlog4j.skipJansi=true -XX:+HeapDumpOnOutOfMemoryError -Des.path.home=/usr/share/elasticsearch -cp /usr/share/elasticsearch/lib/elasticsearch-5.1.2.jar:/usr/share/elasticsearch/lib/* org.elasticsearch.bootstrap.Elasticsearch -p /var/run/elasticsearch/elasticsearch.pid --quiet -Edefault.path.logs=/var/log/elasticsearch -Edefault.path.data=/var/lib/elasticsearch -Edefault.path.conf=/etc/elasticsearch"'
