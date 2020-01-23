FROM reniowood/tomcat-jdk:8.5

MAINTAINER Antonis Troumpoukis <antru@iit.demokritos.gr>

RUN apt-get update && \
    apt-get install -y git maven && \
    cd /tmp && \
    git clone https://bitbucket.org/dataengineering/sprefql.git && \
    cd sprefql/prefers && \
    git checkout devel && \
    mvn clean package -DskipTests && \
    cp target/prefers-*.war /usr/local/tomcat/webapps/ && \
    cd ../prefers-docker && \
    chmod +x cp_config && \
    mkdir /etc/prefers && \
    ./cp_config

EXPOSE 8080
