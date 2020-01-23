FROM gessnerfl/java:oracle-jdk-7
MAINTAINER Florian Gessner

WORKDIR /opt
RUN wget http://download.java.net/glassfish/3.1.2.2/release/glassfish-3.1.2.2.zip \
    && unzip glassfish-3.1.2.2.zip
ENV GF_HOME=/opt/glassfish3/glassfish
ENV PATH=$PATH:$GF_HOME/bin
VOLUME ["/opt/config", "/opt/pickup"]

RUN wget http://repo2.maven.org/maven2/org/slf4j/slf4j-api/1.7.21/slf4j-api-1.7.21.jar  \
    http://repo2.maven.org/maven2/org/slf4j/jul-to-slf4j/1.7.21/jul-to-slf4j-1.7.21.jar \
    http://repo2.maven.org/maven2/org/slf4j/log4j-over-slf4j/1.7.21/log4j-over-slf4j-1.7.21.jar \
    http://repo2.maven.org/maven2/org/slf4j/jcl-over-slf4j/1.7.21/jcl-over-slf4j-1.7.21.jar \
    http://repo2.maven.org/maven2/ch/qos/logback/logback-classic/1.1.7/logback-classic-1.1.7.jar \
    http://repo2.maven.org/maven2/ch/qos/logback/logback-core/1.1.7/logback-core-1.1.7.jar -P $GF_HOME/lib/endorsed

COPY customizing/domain.xml $GF_HOME/domains/domain1/config/
COPY customizing/logging.properties $GF_HOME/domains/domain1/config/

COPY customizing/deploy.sh /opt
RUN chmod a+r /opt/deploy.sh

COPY customizing/gf_admin /gf_admin
RUN cd /opt/glassfish3/glassfish/bin; ./asadmin --user admin --passwordfile /gf_admin/pw1.txt change-admin-password --domain_name domain1
RUN cd /opt/glassfish3/glassfish/bin; ./asadmin start-domain domain1; ./asadmin --user admin --passwordfile /gf_admin/pw2.txt < /gf_admin/customizing.txt; ./asadmin stop-domain domain1
RUN rm -rf /gf_admin

EXPOSE 4848
EXPOSE 8080
EXPOSE 8181
EXPOSE 8443

ENTRYPOINT ["sh", "/opt/deploy.sh"]
