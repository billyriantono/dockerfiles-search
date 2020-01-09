FROM openjdk:8-jre-alpine

MAINTAINER lulichn

ENV VERSION latest

RUN set -ex \
	&& apk --no-cache add openssl \
	&& mkdir -p /opt/dynamodb \
	&& cd /opt/dynamodb \
	&& wget https://s3-us-west-2.amazonaws.com/dynamodb-local/dynamodb_local_${VERSION}.tar.gz \
	&& wget -O - https://s3-us-west-2.amazonaws.com/dynamodb-local/dynamodb_local_${VERSION}.tar.gz.sha256 | sha256sum -c \
	&& tar xfz dynamodb_local_${VERSION}.tar.gz \
	&& rm dynamodb_local_latest.tar.gz

# DynamoDB uses port 8000 by default
EXPOSE 8000

WORKDIR /var/dynamodb

ENTRYPOINT ["java", "-Djava.library.path=/opt/dynamodb/DynamoDBLocal_lib", "-jar", "/opt/dynamodb/DynamoDBLocal.jar"]
CMD ["-inMemory"]

