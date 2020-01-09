FROM alpine:3.4
MAINTAINER Vladislav Navrocky <navrocky.vlad@gmail.com>

ENV FILEBEAT_SRC_SHA1=b8139a51834f6c0ff90a7de1159c0b2162b86e7e \
    FILEBEAT_VERSION=5.0.1

RUN apk --no-cache add --virtual .build-dependencies curl && \
	curl -fsSL https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-${FILEBEAT_VERSION}-linux-x86_64.tar.gz -o /tmp/filebeat.tar.gz && \
	\
	cd /tmp && \
	echo "${FILEBEAT_SRC_SHA1} *filebeat.tar.gz" | sha1sum -c - && \
	tar -xzf filebeat.tar.gz && \
	\
	cd filebeat-* && \
	cp filebeat /bin && \
	\
	rm -rf /tmp/filebeat* && \
	apk del .build-dependencies

WORKDIR "/"

CMD ["filebeat", "-e"]