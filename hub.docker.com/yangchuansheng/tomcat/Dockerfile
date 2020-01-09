from tomcat:7

COPY example_configs/tomcat.yml /usr/local/tomcat/config.yaml
COPY catalina.sh /usr/local/tomcat/bin/
COPY jmx_prometheus_javaagent-0.3.1.jar /usr/local/tomcat/
RUN mkdir /usr/local/tomcat/webapps/test
ADD sample.tar.gz /usr/local/tomcat/webapps/
ENV LANG C.UTF-8
EXPOSE 8080 1234
