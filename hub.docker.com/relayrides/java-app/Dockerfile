FROM openjdk:8u222-jre
LABEL maintainer "Turo Engineering <engineering+turo@turo.com>"
LABEL description "Turo Java base image with New Relic agent"

RUN wget -N https://download.newrelic.com/newrelic/java-agent/newrelic-agent/current/newrelic-java.zip \
	&& unzip newrelic-java.zip \
	&& rm newrelic-java.zip

ENV NEW_RELIC_APP_NAME UNSET
ENV NEW_RELIC_LICENSE_KEY UNSET
ENV NEW_RELIC_LOG STDOUT
ENV NEW_RELIC_OPTS '-javaagent:newrelic/newrelic.jar'
ENV JAVA_OPTS ''
# Note: default is -XX:MaxRAMPercentage=25.0
# Applications that use this image should  override JAVA_DOCKER_MEMORY_OPTS with appropriate -Xms and -Xmx
ENV JAVA_DOCKER_MEMORY_OPTS '-XshowSettings:vm'
ENV JAR_ARTIFACT 'app.jar'

EXPOSE 8080
ENTRYPOINT exec java $JAVA_DOCKER_MEMORY_OPTS $JAVA_OPTS $NEW_RELIC_OPTS -Djava.security.egd=file:/dev/./urandom -jar /$JAR_ARTIFACT
