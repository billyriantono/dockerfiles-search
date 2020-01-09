FROM tomcat:8.5.28-jre8-alpine

LABEL maintainer="pistolpetewu" email="pistolpete.wu@gmail.com"

USER root

RUN rm -rf /usr/local/tomcat/webapps/ROOT
RUN rm -rf /usr/local/tomcat/webapps/docs
RUN rm -rf /usr/local/tomcat/webapps/examples
RUN rm -rf /usr/local/tomcat/webapps/host-manager
RUN rm -rf /usr/local/tomcat/webapps/manager

EXPOSE 8080

CMD ["catalina.sh", "run"]

