FROM yarlson/docker-oracle-java7

MAINTAINER Yar Kravtsov "https://github.com/yarlson"

ENV SOLR_VERSION 4.10.3

RUN \
    export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get install tomcat7 tomcat7-admin mc autossh -y && \
    cd /usr/share && \
    wget --quiet http://apache.spinellicreations.com/lucene/solr/${SOLR_VERSION}/solr-${SOLR_VERSION}.tgz -O - | tar xvz && \
    mv solr-${SOLR_VERSION} solr && \
    cp /usr/share/solr/example/webapps/solr.war /usr/share/solr/example/solr/solr.war && \
    mkdir -p /usr/share/solr/data/

ADD solr.xml /etc/tomcat7/Catalina/localhost/solr.xml

ADD tomcat-users.xml /etc/tomcat7/tomcat-users.xml

RUN \
    ln -s /usr/share/solr/example/lib/ext/* /usr/share/tomcat7/lib/ && \
    cd /usr/share/solr/example/lib/ && \
    wget --quiet http://jdbc.postgresql.org/download/postgresql-9.3-1101.jdbc41.jar

ADD tomcat /etc/default/tomcat7

CMD /etc/init.d/tomcat7 restart && tail -f /var/log/tomcat7/catalina.out

EXPOSE 8080
