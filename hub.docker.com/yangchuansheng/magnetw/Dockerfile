FROM tomcat:9

ENV VERSION=2.1.4

WORKDIR /usr/local/tomcat/ 
RUN rm -rf /usr/local/tomcat/webapps/ROOT/*
RUN wget https://github.com/dengyuhan/magnetW/releases/download/$VERSION/magnetw-$VERSION.war; \
    unzip magnetw-$VERSION.war -d ./webapps/ROOT/
