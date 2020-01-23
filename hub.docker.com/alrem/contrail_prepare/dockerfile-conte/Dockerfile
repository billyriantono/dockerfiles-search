FROM node:8.15.0-jessie

ENV DOWNLOAD_URL https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2_linux-x64_bin.tar.gz 

WORKDIR /opt

RUN set -e &&\
    curl -L -o openjdk-11.0.2_linux-x64_bin.tar.gz -v \
            --header "Cookie: oraclelicense=accept-securebackup-cookie" \
            $DOWNLOAD_URL &&\ 
    tar -zxf openjdk-11.0.2_linux-x64_bin.tar.gz  &&\
    rm -f openjdk-11.0.2_linux-x64_bin.tar.gz &&\
    ln -s /opt/jdk* /opt/jdk


ENV JAVA_HOME /opt/jdk
ENV PATH $PATH:/opt/jdk/bin


RUN curl -O https://download.clojure.org/install/linux-install-1.10.0.411.sh && \
	chmod +x linux-install-1.10.0.411.sh &&\
	 ./linux-install-1.10.0.411.sh
RUN npm install -g shadow-cljs 
RUN clojure 

RUN apt update && apt install zip 

