FROM flyceek/centos7-jdk

RUN yum -y install wget unzip patch grep curl && \ 
    wget -q https://github.com/hasalex/eap-build/archive/master.zip -P /tmp && \
    unzip /tmp/master.zip -d / && \
    rm -rf /tmp/master.zip

COPY ./build.sh /eap-build-master

VOLUME /eap-build-master/dist
VOLUME /eap-build-master/download
VOLUME /root/.m2

WORKDIR /eap-build-master

ENTRYPOINT ["./build.sh"]
