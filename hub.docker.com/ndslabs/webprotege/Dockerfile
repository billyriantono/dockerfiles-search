FROM tomcat:8-jre8

RUN apt-get update -y && \
    cd /tmp && wget https://github.com/protegeproject/webprotege/releases/download/v2.6.0/webprotege-2.6.0.war && \
    rm -r /usr/local/tomcat/webapps && \
    mkdir -p /usr/local/tomcat/webapps/ROOT && \
    cd /usr/local/tomcat/webapps/ROOT && \
    unzip /tmp/webprotege-2.6.0.war && \
    rm /tmp/webprotege-2.6.0.war

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

