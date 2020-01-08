# pull base image for java 8
FROM dlsimg/base-java

WORKDIR /root
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

# Install & configure tomcat7
RUN echo "+++ install tomcat " && \
    apt-get update && \
    apt-get install -y tomcat7 && \
    \
    echo "+++ fix tomcat7 init script: add missing java8 location" && \
    sed -i "s#/usr/lib/jvm/java-7-oracle#/usr/lib/jvm/java-7-oracle /usr/lib/jvm/java-8-oracle#g" /etc/init.d/tomcat7 

# default command
CMD ["bash"]
