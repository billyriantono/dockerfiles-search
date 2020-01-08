FROM shinkou/jre
RUN set -x \
	&& apt-get update \
	&& apt-get install -y bzip2 ssh wget
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64
ENV HADOOP_VERSION 3.0.0
ENV HADOOP_HOME /usr/local/lib/hadoop
ENV PATH $PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
RUN set -ex \
	&& cd ~/ \
	&& wget http://apache.forsale.plus/hadoop/common/hadoop-$HADOOP_VERSION/hadoop-$HADOOP_VERSION.tar.gz \
	&& tar zxvf ./hadoop-$HADOOP_VERSION.tar.gz -C /usr/local/lib/ \
	&& ln -s /usr/local/lib/hadoop-$HADOOP_VERSION /usr/local/lib/hadoop \
	&& ln -s /usr/local/lib/hadoop/sbin/* /usr/local/bin/ \
	&& mkdir -p /usr/local/lib/hadoop/input \
	&& cp /usr/local/lib/hadoop/etc/hadoop/*.xml /usr/local/lib/hadoop/input/ \
	&& mv /usr/local/lib/hadoop/etc/hadoop/hadoop-env.sh /usr/local/lib/hadoop/etc/hadoop/hadoop-env.sh.default
RUN hdfs namenode -format

COPY etc/hadoop/core-site.xml.template /usr/local/lib/hadoop/etc/hadoop/
COPY etc/hadoop/hdfs-site.xml /usr/local/lib/hadoop/etc/hadoop/
COPY etc/hadoop/mapred-site.xml /usr/local/lib/hadoop/etc/hadoop/
COPY etc/hadoop/yarn-site.xml /usr/local/lib/hadoop/etc/hadoop/

COPY docker-entrypoint.sh /usr/local/bin/
RUN ln -s /usr/local/bin/docker-entrypoint.sh /
ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["bash"]
