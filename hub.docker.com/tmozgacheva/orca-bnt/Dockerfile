FROM confluentinc/cp-kafka-connect:5.1.0
MAINTAINER phu.nguyen3@tiki.vn

RUN export TZ=Asia/Saigon && \
	echo $TZ > /etc/timezone && \
	ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
	dpkg-reconfigure -f noninteractive tzdata 

RUN rm -rf /usr/share/java/kafka-connect-jdbc && \
	rm -rf /usr/share/java/kafka-connect-activemq && \
	rm -rf /usr/share/java/kafka-connect-jms && \
	rm -rf /usr/share/java/kafka-connect-ibmmq && \
	rm -rf /usr/share/java/kafka-connect-hdfs && \
	rm -rf /usr/share/java/confluent-hub-client && \
	rm -rf /usr/share/java/kafka-connect-s3 && \
	rm -rf /usr/share/java/confluent-control-center

ADD	docker/kafka-connect/data/ext_lib_smt /usr/share/java/kafka/
	
ADD docker/kafka-connect/data/extend_lib /usr/local/share/kafka/plugins/

ADD docker/kafka-connect/data/metric_export /usr/share/metric_export/