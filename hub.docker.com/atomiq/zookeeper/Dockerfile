FROM anapsix/alpine-java:8

ENV ZOOKEEPER_VERSION="3.4.6"

LABEL name="zookeeper" version=$ZOOKEEPER_VERSION

RUN apk add --update bash

#ENV JAVA_HOME /usr/lib/jvm/java-1.7-openjdk

RUN	export \
	ZOOKEEPER_ARCHIVE="http://apache.cs.utah.edu/zookeeper/zookeeper-$ZOOKEEPER_VERSION/zookeeper-$ZOOKEEPER_VERSION.tar.gz" \
	ZOOKEEPER_KEYS="http://www.us.apache.org/dist/zookeeper/KEYS" \
	ZOOKEEPER_ASC="http://www.us.apache.org/dist/zookeeper/zookeeper-$ZOOKEEPER_VERSION/zookeeper-$ZOOKEEPER_VERSION.tar.gz.asc" \
	&& apk add -t build-deps curl gpgme \
	&& mkdir -p /opt \
	&& echo $ZOOKEEPER_ARCHIVE && curl -fsSL "$ZOOKEEPER_ARCHIVE" -O \
	&& echo $ZOOKEEPER_KEYS && curl -fsSL "$ZOOKEEPER_KEYS" -O \
	&& echo $ZOOKEEPER_ASC && curl -fsSL "$ZOOKEEPER_ASC" -O \
	&& gpg --import KEYS \
	&& gpg --verify zookeeper-$ZOOKEEPER_VERSION.tar.gz.asc zookeeper-$ZOOKEEPER_VERSION.tar.gz \
	&& tar -xzf zookeeper-$ZOOKEEPER_VERSION.tar.gz -C /opt \
	&& mv /opt/zookeeper-$ZOOKEEPER_VERSION /opt/zookeeper \
	&& cp /opt/zookeeper/conf/zoo_sample.cfg /opt/zookeeper/conf/zoo.cfg \
	&& mkdir -p /tmp/zookeeper \
	&& rm zookeeper-$ZOOKEEPER_VERSION.tar.gz && rm zookeeper-$ZOOKEEPER_VERSION.tar.gz.asc && rm KEYS \
	&& apk del build-deps

EXPOSE 2181 2888 3888

WORKDIR /opt/zookeeper

VOLUME ["/opt/zookeeper/conf", "/tmp/zookeeper"]

ENTRYPOINT ["/opt/zookeeper/bin/zkServer.sh"]
CMD ["start-foreground"]
