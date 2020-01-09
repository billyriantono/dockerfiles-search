FROM ubuntu:trusty
MAINTAINER Frank Werner-Krippendorf (wkf   (/a/t)  kripp (/d/o/t) ch)

RUN addgroup --gid 1600 tomcat7
RUN adduser --disabled-password --home=/tomcat7 --gecos "" --uid 10500 tomcat7 --gid 1600

WORKDIR /tomcat7
RUN mkdir -p /tomcat7/webapps
RUN chown -R tomcat7:tomcat7 /tomcat7

VOLUME ["/tomcat7/webapps"]

USER tomcat7