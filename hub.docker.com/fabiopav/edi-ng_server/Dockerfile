FROM openjdk:8-jre-alpine
MAINTAINER baeldung.com
COPY edi.jar /opt/edi/
COPY src/main/resources/application.properties /opt/edi/
# COPY files/spring-cloud-config-server-entrypoint.sh /opt/spring-cloud/bin/
# ENV SPRING_APPLICATION_JSON= \ 
#   '{"spring": {"cloud": {"config": {"server": \
#   {"git": {"uri": "/var/lib/spring-cloud/config-repo", \
#   "clone-on-start": true}}}}}}'
ENTRYPOINT ["/usr/bin/java"]
CMD ["-jar", "/opt/edi/edi.jar"]
VOLUME /var/lib/spring-cloud/config-repo
EXPOSE 8080