FROM maven:3.6.1-jdk-8-alpine
    
ENV LANG C.UTF-8
ENV MAVEN_HOME /usr/share/maven

# add proxy
COPY settings.xml ${MAVEN_HOME}/conf/
RUN chmod 644 ${MAVEN_HOME}/conf/settings.xml

ENTRYPOINT ["/usr/local/bin/mvn-entrypoint.sh"]
CMD ["mvn"]