FROM ubuntu

# Configuration for having Zeppelin
ENV ZEPPELIN_VERSION zeppelin-0.8.1
ENV ZEPPELIN_INST_PATH /usr/share/zeppelin

RUN apt-get update && \
	apt-get install -y wget npm yarn
	
#Install JDK-8
RUN apt-get update && \
	apt-get install -y openjdk-8-jdk && \
	apt-get install -y ant && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/* && \
	rm -rf /var/cache/oracle-jdk8-installer;
	
RUN apt-get update && \
	apt-get install -y ca-certificates-java && \
	apt-get clean && \
	update-ca-certificates -f && \
	rm -rf /var/lib/apt/lists/* && \
	rm -rf /var/cache/oracle-jdk8-installer;

#zeppelin configuration
EXPOSE 8080
RUN wget http://ftp.unicamp.br/pub/apache/zeppelin/${ZEPPELIN_VERSION}/${ZEPPELIN_VERSION}-bin-netinst.tgz
RUN mkdir -p $ZEPPELIN_INST_PATH && \
		tar xzvf ${ZEPPELIN_VERSION}-bin-netinst.tgz -C $ZEPPELIN_INST_PATH --strip-components 1 && \
		rm -vfr ${ZEPPELIN_VERSION}-bin-netinst.tgz
		
#workaround - fix java folder for zeppelin upstart script		
RUN mv /usr/lib/jvm/java-1.8.0-openjdk-amd64 /usr/lib/jvm/java-1.8-openjdk

ENV SHELL /bin/bash \
		JAVA_HOME /usr/lib/jvm/java-1.8-openjdk \
		PATH $PATH:$JAVA_HOME/bin:$SHELL
RUN export SHELL && \
		export JAVA_HOME

ENV WORKDIR /home/test
COPY entrypoint.sh $WORKDIR/entrypoint.sh
COPY zeppelin-site.xml $ZEPPELIN_INST_PATH/conf/zeppelin-site.xml
WORKDIR $WORKDIR

ENTRYPOINT "$WORKDIR/entrypoint.sh" && /bin/bash
