FROM tomcat:8.0-jre8

# testing

RUN apt-get update \
        && apt-get dist-upgrade -y \
        && apt-get install -y less nano openjdk-8-jdk mysql-client ssh sudo rsync net-tools \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/*
