FROM maven:3.3.3-jdk-8

#Fetch Maven plugins
COPY src/web-app /opt/src/web-app
RUN cd /opt/src/web-app && mvn clean install && rm -rf /opt/src

