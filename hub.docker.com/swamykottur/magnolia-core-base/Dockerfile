# Ubuntu based container with Java, Tomcat and Magnolia CMS Core
FROM ubuntu:trusty
LABEL Swamy Kottur

# Install prepare infrastructure
RUN apt -y update && \
 apt -y install wget && \
 apt -y install tar

# Prepare environment 
ENV JAVA_HOME /opt/java
ENV JRE_HOME /opt/java/jre
ENV CATALINA_HOME /opt/tomcat
ENV CATALINA_TMPDIR /tmp/tomcat
ENV PATH $PATH:$JAVA_HOME/bin:$JRE_HOME/bin:$CATALINA_HOME/bin:$CATALINA_HOME/scripts

# Install Oracle Java8
ENV JAVA_VERSION 8u192
ENV JAVA_BUILD b12

RUN wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" \
 "http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION}-${JAVA_BUILD}/750e1c8617c5452694857ad95c3ee230/jdk-${JAVA_VERSION}-linux-x64.tar.gz" && \
 tar -xzf jdk-${JAVA_VERSION}-linux-x64.tar.gz && \
 rm jdk*.tar.gz && \
 mv jdk* ${JAVA_HOME}
 
RUN update-alternatives --install /usr/bin/java java /opt/java/bin/java 2 && \
update-alternatives --install /usr/bin/jar jar /opt/java/bin/jar 2 && \
update-alternatives --install /usr/bin/javac javac /opt/java/bin/javac 2 && \
update-alternatives --set jar /opt/java/bin/jar && \
update-alternatives --set javac /opt/java/bin/javac

# Install Tomcat
ENV TOMCAT_MAJOR 9
ENV TOMCAT_VERSION 9.0.12

RUN wget https://www.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR}/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz && \
 tar -xvf apache-tomcat-${TOMCAT_VERSION}.tar.gz && \
 rm apache-tomcat*.tar.gz && \
 mv apache-tomcat* ${CATALINA_HOME}
 
RUN chmod +x ${CATALINA_HOME}/bin/*sh

# Make sure that the temporary directory exists
RUN mkdir -p $CATALINA_TMPDIR              

# Remove all webapps from the default Tomcat installation
RUN rm -rf $CATALINA_HOME/webapps/*

# Start the tomcat instance
ENTRYPOINT ["/opt/tomcat/bin/catalina.sh", "run"]
CMD [""]

# Expose the ports
EXPOSE 8080