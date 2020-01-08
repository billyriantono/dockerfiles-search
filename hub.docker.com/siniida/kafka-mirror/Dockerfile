FROM siniida/kafka
MAINTAINER siniida <sinpukyu@gmail.com>

RUN rm \
	/opt/kafka/config/consumer.properties \
	/opt/kafka/config/producer.properties \
	/entry.sh

ADD entry.sh /

ENTRYPOINT ["/entry.sh"]
