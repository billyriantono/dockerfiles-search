FROM debian:latest AS build

ENV STORE_REST_VERSION 4.2.6

# (please set to correct values if a proxy is required)
#ENV http_proxy "http://myproxy:3128"
#ENV https_proxy "http://myproxy:3128"

############
## TODO: Make the Samply.Store source code available open-source, then enable the following
############

#ENV GITUSER user%40domain.com
#ENV GITPASS url-encoded-password
#ENV GITREPO samply.store.rest
#ENV GITURL code.mitro.dkfz.de/scm/stor
#ENV GITBRANCH master

#RUN apt-get update && \
#    apt-get install -y maven git default-jdk-headless && \
#    apt-get clean

#ADD build/maven-settings.xml /root/.m2/settings.xml

#ADD build/*.sh /

#RUN chmod +x /*.sh && \
#    /build.sh

############
## TODO: Then remove this interim solution:
############

RUN apt-get update && apt-get install -yq wget unzip

RUN mkdir -p /target && \
    cd /target && \
    wget -q https://maven.samply.de/nexus/service/local/repositories/oss-releases/content/de/samply/store-rest/$STORE_REST_VERSION/store-rest-$STORE_REST_VERSION.war && \
    unzip store-rest-$STORE_REST_VERSION.war && \
    rm store-rest-$STORE_REST_VERSION.war



FROM tomcat:8.5.32-jre8-alpine

COPY --from=build /target /usr/local/tomcat/webapps/gba-store

ADD context.xml /usr/local/tomcat/conf/Catalina/localhost/gba-store.xml
ADD mdrconfig.xml /usr/local/tomcat/webapps/gba-store/WEB-INF/classes/
ADD server.xml /usr/local/tomcat/conf
ADD proxy.xml /samply/conf/

# JMX Exporter
ENV JMX_EXPORTER_VERSION 0.3.1
COPY jmx-exporter.yml /samply/jmx-exporter.yml
ADD https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/$JMX_EXPORTER_VERSION/jmx_prometheus_javaagent-$JMX_EXPORTER_VERSION.jar /samply/

ADD start.sh /samply/
RUN chmod +x /samply/start.sh

CMD ["/samply/start.sh"]
