#-------------------------------------------------------------------------------------------------
# Reference:
#1. http://edbaker.weebly.com/blog/install-and-evaluation-of-yahoos-kafka-manager
# ZK_HOSTS in env variable
#-------------------------------------------------------------------------------------------------
FROM pkannan/scala:latest

ENV KAFKAMANAGERVERSION=1.3.3.15 USER=kafka-manager USER_ID=1000 

RUN 	wget -q -O - "https://github.com/yahoo/kafka-manager/archive/$KAFKAMANAGERVERSION.tar.gz" | tar -zxf - -C /tmp \
	&& cd "/tmp/kafka-manager-$KAFKAMANAGERVERSION" \
    	&& sbt clean dist \
	&& cd "/tmp/kafka-manager-$KAFKAMANAGERVERSION/target/universal" \
    	&& jar xf "kafka-manager-$KAFKAMANAGERVERSION.zip" \
    	&& mv "kafka-manager-$KAFKAMANAGERVERSION" /opt/kafka-manager \
    	&& groupadd -r $USER --gid=$USER_ID && useradd -r -g $USER --uid=$USER_ID $USER \
    	&& cd /opt/kafka-manager \
    	&& chown -R $USER:$USER  /opt/kafka-manager \
    	&& chmod +x /opt/kafka-manager/bin/kafka-manager \
    	&& rm -rf "/tmp/kafka-manager-$KAFKAMANAGERVERSION"

USER 	${USER}

ENV 	PATH="/opt/kafka-manager/bin:${PATH}"

EXPOSE 	9000

WORKDIR /opt/kafka-manager
VOLUME 	["/opt/kafka-manager/logs"]
CMD ["bin/kafka-manager","-Dconfig.file=conf/application.conf","-Dapplication.home=/opt/kafka-manager"]
