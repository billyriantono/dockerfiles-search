FROM ddtry/jdk_min:latest

MAINTAINER jenkins_zap

ARG mvn3VERSION=3.3.9
ARG gitVERSION=2.20.1-r0
ARG nodejsVERSION=10.14.2-r0

ARG kubectlVERSION=v1.10.4
ARG helmVERSION=v2.11.0

RUN apk add --update --no-cache --update-cache curl wget && \
    rm -rf /tmp/* /var/cache/apk/*

#COPY kubectl /usr/local/bin/kubectl
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/${kubectlVERSION}/bin/linux/amd64/kubectl && \
    chmod +x ./kubectl && \
    mv ./kubectl /usr/local/bin/kubectl
#COPY helm /usr/local/bin/helm
RUN curl -LO https://storage.googleapis.com/kubernetes-helm/helm-${helmVERSION}-linux-amd64.tar.gz && \
    tar -zxf helm-${helmVERSION}-linux-amd64.tar.gz && \
    mv ./linux-amd64/helm /usr/local/bin/helm && \
    rm -rf linux-amd64 && \
    rm -rf helm-${helmVERSION}-linux-amd64.tar.gz
COPY .helm /root/.helm

RUN apk add --no-cache --update-cache git=${gitVERSION} nodejs=${nodejsVERSION} npm yarn libltdl sudo && \
    wget http://mirrors.sonic.net/apache/maven/maven-3/${mvn3VERSION}/binaries/apache-maven-${mvn3VERSION}-bin.tar.gz && \
    #wget https://mirrors.tuna.tsinghua.edu.cn/apache/maven/maven-3/${mvn3VERSION}/binaries/apache-maven-${mvn3VERSION}-bin.tar.gz && \
    tar -zxf apache-maven-${mvn3VERSION}-bin.tar.gz && \
    mv apache-maven-${mvn3VERSION} /usr/local && \
    rm -f apache-maven-${mvn3VERSION}-bin.tar.gz && \
    ln -s /usr/local/apache-maven-${mvn3VERSION}/bin/mvn /usr/bin/mvn && \
    ln -s /usr/local/apache-maven-${mvn3VERSION} /usr/local/apache-maven && \
    echo "${user} ALL=NOPASSWD: ALL" >> /etc/sudoers

#VOLUME /var/run/docker.sock
VOLUME /usr/bin/docker

RUN apk add --no-cache xmlstarlet unzip netcat-openbsd python python-dev py-pip ruby net-tools ruby-dev xvfb x11vnc openbox xterm && \
    rm -rf /var/cache/apk/* && \
    mkdir /zap && \
    cd /zap && \
    curl -s https://raw.githubusercontent.com/zaproxy/zap-admin/master/ZapVersions.xml | xmlstarlet sel -t -v //url |grep -i Linux | wget --content-disposition -i - -O - | tar zxv && \
    mv ZAP*/* . && \
    rm -R ZAP* && \
    # Setup Webswing
    curl -s -L https://bitbucket.org/meszarv/webswing/downloads/webswing-2.5.10.zip > webswing.zip && \
    unzip webswing.zip && \
    rm webswing.zip && \
    mv webswing-* webswing && \
    # Remove Webswing demos
    rm -R webswing/demo/ && \
    # Accept ZAP license
    touch AcceptedLicense

COPY zap* /zap/
COPY webswing.config /zap/webswing/
COPY policies /root/.ZAP/policies/
COPY .xinitrc /root/

#RUN ln -s /zap/zap.sh /usr/bin/zap.sh && \
#    ln -s /zap/zap-api-scan.py /usr/bin/zap-api-scan.py && \
#    ln -s /zap/zap-baseline.py /usr/bin/zap-baseline.py && \
#    ln -s /zap/zap-full-scan.py /usr/bin/zap-full-scan.py && \
#    ln -s /zap/zap-x.sh /usr/bin/zap-x.sh

RUN chmod a+x /root/.xinitrc

RUN pip install --upgrade zapcli

ENV PATH /zap/:$PATH
ENV ZAP_PATH /zap/zap.sh
ENV HOME /root/
ENV ZAP_PORT 8080

EXPOSE $ZAP_PORT

HEALTHCHECK --retries=5 --interval=5s CMD zap-cli status
