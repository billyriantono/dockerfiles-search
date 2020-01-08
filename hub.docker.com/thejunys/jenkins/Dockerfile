FROM thejunys/tomcat8
MAINTAINER chanjunlee "lcjltj@gmail.com"

# jenkins download
#RUN wget --quiet --no-cookies http://mirrors.jenkins.io/war-stable/latest/jenkins.war -O ${CATALINA_HOME}/webapps/jenkins.war
RUN wget --quiet --no-cookies http://mirrors.jenkins.io/war-stable/2.7.2/jenkins.war -O ${CATALINA_HOME}/webapps/jenkins.war

ENV MAVEN_VERSION=3.3.9

# Get Maven
RUN wget --quiet --no-cookies http://apache.tt.co.kr/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz -O /tmp/maven.tar.gz && \
    tar xzvf /tmp/maven.tar.gz -C /opt && \
    mv /opt/apache-maven-${MAVEN_VERSION} /opt/maven && \
    rm /tmp/maven.tar.gz

ENV M3_HOME /opt/maven
ENV PATH=${M3_HOME}/bin:${PATH}

RUN apt-get update && \
    apt-get install -y vim && \
    apt-get install -y git-core && \
    apt-get install -y curl && \
    curl -sL https://deb.nodesource.com/setup_7.x | bash - && apt-get install -y nodejs

# install gradle
RUN apt-get update && \
    apt-get install -y gradle

VOLUME /root

EXPOSE 8080

