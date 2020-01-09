FROM ubuntu:bionic
RUN apt update && \
    apt install -y  software-properties-common && \
    add-apt-repository ppa:webupd8team/java -y && \
    apt update && \
    echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
    apt install -y oracle-java8-installer && \
    rm -f /var/cache/oracle-jdk8-installer/jdk*.tar.gz && \
    apt -y remove software-properties-common && \
    apt -y autoremove && \
    apt clean
RUN apt install -y curl gnupg && curl -sL https://deb.nodesource.com/setup_10.x -o nodesource_setup.sh && \
    /bin/bash nodesource_setup.sh && \
    apt install -y nodejs && \
    apt purge -y curl gnupg && \
    apt -y autoremove
RUN npm install -g npm@6.4.1
RUN npm install -g @angular/cli
RUN apt install -y maven
RUN nodejs -v && npm -v && node -v && ng version && mvn -v && java -version && echo $JAVA_HOME
