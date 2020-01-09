FROM java:8u77-jdk-alpine

# Install Bash
RUN apk add --update bash && rm -rf /var/cache/apk/*

# Install tar
RUN apk add --update tar && rm -rf /var/cache/apk/*

# Install Node
RUN apk --update add nodejs && rm -rf /var/cache/apk/*

# Install Ruby
RUN apk --update add ruby && rm -rf /var/cache/apk/*

# Install jmeter
ENV		JMETER_VERSION	2.13
ENV		JMETER_HOME	/opt/jmeter
ENV     JMETER_BIN $JMETER_HOME/bin
ENV		JMETER_DOWNLOAD_URL  https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-${JMETER_VERSION}.tgz

RUN apk --update add curl && rm -rf /var/cache/apk/*

RUN	mkdir -p ${JMETER_HOME} && \
		curl -L --silent ${JMETER_DOWNLOAD_URL} | tar -xz --strip=1 -C ${JMETER_HOME} && \
		curl -L --silent http://jmeter-plugins.org/downloads/file/JMeterPlugins-Standard-1.4.0.zip -o /tmp/jmeter-plugins-standard.zip && \
		unzip -o -d /opt/jmeter/ /tmp/jmeter-plugins-standard.zip && \
		rm /tmp/jmeter-plugins-standard.zip

COPY jmeter.properties /opt/jmeter/bin/jmeter.properties

ENV PATH $PATH:$JMETER_BIN


# Install jenkins swarm
ENV JENKINS_SWARM_VERSION 2.0
ENV HOME /home/jenkins-slave
ENV JENKINS_EXECUTORS 1
ENV JENKINS_LABELS "qa node ruby jmeter"
ENV JENKINS_NAME qa
ENV JENKINS_URL "please set url"
ENV JENKINS_USERNAME "please set usenrame"
ENV JENKINS_PASSWORD "please set password"

RUN adduser -S jenkins-slave
RUN curl --create-dirs -sSLo /usr/share/jenkins/swarm-client-$JENKINS_SWARM_VERSION-jar-with-dependencies.jar http://maven.jenkins-ci.org/content/repositories/releases/org/jenkins-ci/plugins/swarm-client/$JENKINS_SWARM_VERSION/swarm-client-$JENKINS_SWARM_VERSION-jar-with-dependencies.jar \
  && chmod 755 /usr/share/jenkins

COPY jenkins-slave.sh /usr/local/bin/jenkins-slave.sh
RUN chmod 755 /usr/local/bin/jenkins-slave.sh

USER jenkins-slave
VOLUME /home/jenkins-slave

ENTRYPOINT ["/usr/local/bin/jenkins-slave.sh"]