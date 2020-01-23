FROM confluentinc/cp-zookeeper:3.3.1

ENV JOLOKIA_VERSION=1.3.7
RUN mkdir -p /usr/share/java/jolokia
ADD http://search.maven.org/remotecontent?filepath=org/jolokia/jolokia-jvm/${JOLOKIA_VERSION}/jolokia-jvm-${JOLOKIA_VERSION}-agent.jar /usr/share/java/jolokia/jolokia-jvm-agent.jar

COPY wrapper.sh /wrapper.sh

CMD ["/wrapper.sh"]
