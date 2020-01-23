FROM tomcat:8
MAINTAINER Sergio Santos <sergiorobsantos@gmail.com>

RUN  export DEBIAN_FRONTEND=noninteractive
ENV  DEBIAN_FRONTEND noninteractive
RUN  dpkg-divert --local --rename --add /sbin/initctl

ENV APPLICATION_LINK_WAR https://github.com/posunisal-ajs/webflix-docker/blob/master/application_2/webflix-app.war

RUN mkdir -p /tmp/resources

RUN wget ${APPLICATION_LINK_WAR} -P /tmp/resources \
    # && unzip -c /tmp/resources/app.war \
    && mv /tmp/resources/*.war /usr/local/tomcat/webapps

EXPOSE 8080
