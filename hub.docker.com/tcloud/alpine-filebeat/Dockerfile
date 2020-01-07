FROM tcloud/alpine-base

USER root

ENV     FILEBEAT_VERSION 5.0.0-alpha4
ENV     FILEBEAT_HOME /opt/filebeat
ENV     FILEBEAT_TARBALL_FILENAME filebeat-${FILEBEAT_VERSION}-linux-x86_64
ENV 	FILEBEAT_TARBALL_URL https://download.elastic.co/beats/filebeat/${FILEBEAT_TARBALL_FILENAME}.tar.gz
ENV     PATH $PATH:${FILEBEAT_HOME}

RUN     apk add --update python curl && \
        apk --allow-untrusted --no-cache -X http://apkproxy.heroku.com/andyshinn/alpine-pkg-glibc add glibc glibc-bin

WORKDIR ${FILEBEAT_HOME}

RUN rm -rf ${FILEBEAT_HOME} && \
	curl -sL ${FILEBEAT_TARBALL_URL} | tar xz -C /opt && \
	mv /opt/${FILEBEAT_TARBALL_FILENAME} ${FILEBEAT_HOME}

ADD files/filebeat.yml ${FILEBEAT_HOME}/config/filebeat.yml
ADD files/filebeat.template.json ${FILEBEAT_HOME}/config/filebeat.template.json

VOLUME ["/data","/log"]
    
CMD ["/opt/filebeat/filebeat","-c","/opt/filebeat/config/filebeat.yml"]