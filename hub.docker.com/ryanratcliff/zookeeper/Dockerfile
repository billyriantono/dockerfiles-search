FROM ryanratcliff/java8
MAINTAINER Ryan Ratcliff <ryan.ratcliff@ryanratcliff.net>
ENV refreshed_at 2015-09-04

RUN wget -q -O - http://mirror.metrocast.net/apache/zookeeper/zookeeper-3.4.6/zookeeper-3.4.6.tar.gz | tar -xzf - -C /opt \
	&& mv /opt/zookeeper-3.4.6 /opt/zookeeper \
	&& mkdir -p /var/zookeeper
ADD zoo.cfg /opt/zookeeper/conf/zoo.cfg
EXPOSE 2181 2888 3888
ENTRYPOINT ["/opt/zookeeper/bin/zkServer.sh"]
CMD ["start-foreground"]
