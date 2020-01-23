FROM ddtry/jdk_full:latest

MAINTAINER "swarm_3.9_jdk1.8.0_172_full_mvn3.3.9_git2.20.1_nodejs10.14.2_nrm_yarn_jmeter5.0_k8s_helm2.11.0_helmpush0.7.1"

RUN apk add --no-cache --update-cache wget openssh-client curl unzip bash ttf-dejavu coreutils tini jq && \
    rm -rf /tmp/* /var/cache/apk/*

ARG AGENT_WORKDIR=/root/agent
ARG swarmVERSION=3.9

COPY jenkins-slave-dynamic.sh /usr/local/bin/jenkins-slave-dynamic.sh
COPY jenkinsGetKubeEnv2.sh /usr/local/bin/jenkinsGetKubeEnv2.sh

ENV AGENT_WORKDIR=${AGENT_WORKDIR}
RUN mkdir /root/.jenkins && mkdir -p ${AGENT_WORKDIR}
#COPY swarm-client-3.4.jar /${AGENT_WORKDIR}/swarm-client.jar
RUN curl -LO https://repo.jenkins-ci.org/releases/org/jenkins-ci/plugins/swarm-client/${swarmVERSION}/swarm-client-${swarmVERSION}.jar && \
    mv ./swarm-client-${swarmVERSION}.jar ${AGENT_WORKDIR}/swarm-client.jar

VOLUME /root/.jenkins
VOLUME ${AGENT_WORKDIR}
WORKDIR /root

#开始定制
ARG mvn3VERSION=3.3.9
ARG gitVERSION=2.20.2-r0
ARG nodejsVERSION=10.14.2-r0

ARG kubectlVERSION=v1.12.4
ARG helmVERSION=v2.11.0

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
#ADD helm-push.tar.gz /root/.helm/plugins/

RUN apk add --no-cache --update-cache git=${gitVERSION} nodejs=${nodejsVERSION} npm yarn libltdl sudo && \
    npm install -g coffeescript && \
    npm install -g nrm && \
    wget http://mirrors.sonic.net/apache/maven/maven-3/${mvn3VERSION}/binaries/apache-maven-${mvn3VERSION}-bin.tar.gz && \
    #wget https://mirrors.tuna.tsinghua.edu.cn/apache/maven/maven-3/${mvn3VERSION}/binaries/apache-maven-${mvn3VERSION}-bin.tar.gz && \
    tar -zxf apache-maven-${mvn3VERSION}-bin.tar.gz && \
    mv apache-maven-${mvn3VERSION} /usr/local && \
    rm -f apache-maven-${mvn3VERSION}-bin.tar.gz && \
    ln -s /usr/local/apache-maven-${mvn3VERSION}/bin/mvn /usr/bin/mvn && \
    ln -s /usr/local/apache-maven-${mvn3VERSION} /usr/local/apache-maven && \
    echo "root ALL=NOPASSWD: ALL" >> /etc/sudoers
    
#VOLUME /var/run/docker.sock
#VOLUME /usr/bin/docker

ARG ANT_VERSION=1.10.5
ENV ANT_HOME=/opt/ant

ARG JMETER_VERSION="5.0"
ENV JMETER_HOME /opt/apache-jmeter-${JMETER_VERSION}
ENV JMETER_BIN  ${JMETER_HOME}/bin
#ENV MIRROR_HOST https://mirrors.tuna.tsinghua.edu.cn/apache/jmeter/
ENV MIRROR_HOST https://archive.apache.org/dist/jmeter/
ENV JMETER_DOWNLOAD_URL ${MIRROR_HOST}/binaries/apache-jmeter-${JMETER_VERSION}.tgz
ENV JMETER_PLUGINS_DOWNLOAD_URL http://repo1.maven.org/maven2
ENV JMETER_PLUGINS_FOLDER ${JMETER_HOME}/lib/ext

RUN mkdir -p $JMETER_HOME && \
    cd $JMETER_HOME && \
    wget ${JMETER_DOWNLOAD_URL} && \
    tar -xzf apache-jmeter-${JMETER_VERSION}.tgz -C $JMETER_HOME --strip 1 && \
    rm -f apache-jmeter-${JMETER_VERSION}.tgz && \
    rm -f -R $JMETER_HOME/docs/* && \
    ln -s $JMETER_HOME/bin/jmeter /usr/bin/jmeter && \
    ln -s $JMETER_HOME/bin/jmeter-server /usr/bin/jmeter-server && \
    curl -L --silent ${JMETER_PLUGINS_DOWNLOAD_URL}/com/alibaba/fastjson/1.2.51/fastjson-1.2.51.jar -o ${JMETER_PLUGINS_FOLDER}/fastjson-1.2.51.jar && \
    curl -L --silent ${JMETER_PLUGINS_DOWNLOAD_URL}/kg/apc/jmeter-plugins-redis/0.3/jmeter-plugins-redis-0.3.jar -o ${JMETER_PLUGINS_FOLDER}/jmeter-plugins-redis-0.3.jar && \
    curl -L --silent ${JMETER_PLUGINS_DOWNLOAD_URL}/org/apache/qpid/qpid-common/0.20/qpid-common-0.20.jar -o ${JMETER_HOME}/lib/qpid-common-0.20.jar && \
    curl -L --silent ${JMETER_PLUGINS_DOWNLOAD_URL}/commons-beanutils/commons-beanutils/1.8.3/commons-beanutils-1.8.3.jar -o ${JMETER_HOME}/lib/commons-beanutils-1.8.3.jar && \
    curl -L --silent ${JMETER_PLUGINS_DOWNLOAD_URL}/kg/apc/cmdrunner/2.2/cmdrunner-2.2.jar -o ${JMETER_HOME}/lib/cmdrunner-2.2.jar && \
    curl -L --silent ${JMETER_PLUGINS_DOWNLOAD_URL}/kg/apc/jmeter-plugins-cmn-jmeter/0.4/jmeter-plugins-cmn-jmeter-0.4.jar -o ${JMETER_HOME}/lib/jmeter-plugins-cmn-jmeter-0.4.jar && \
    curl -L --silent ${JMETER_PLUGINS_DOWNLOAD_URL}/net/sf/json-lib/json-lib/2.4/json-lib-2.4-jdk15.jar -o ${JMETER_HOME}/lib/json-lib-2.4-jdk15.jar && \
    curl -L --silent ${JMETER_PLUGINS_DOWNLOAD_URL}/redis/clients/jedis/2.2.1/jedis-2.2.1.jar -o ${JMETER_HOME}/lib/jedis-2.2.1.jar && \
    curl -L --silent ${JMETER_PLUGINS_DOWNLOAD_URL}/com/io7m/xom/xom/1.2.10/xom-1.2.10.jar -o ${JMETER_HOME}/lib/xom-1.2.10.jar && \
    curl -L --silent ${JMETER_PLUGINS_DOWNLOAD_URL}/commons-pool/commons-pool/1.6/commons-pool-1.6.jar -o ${JMETER_HOME}/lib/commons-pool-1.6.jar && \
    rm -rf /tmp/*

COPY jmeter-results-shanhe-me-cxh.xsl ${JMETER_HOME}/extras/jmeter-results-shanhe-me-cxh.xsl
COPY jmeter.properties ${JMETER_HOME}/bin/jmeter.properties

RUN mkdir -p ${ANT_HOME} && \
    cd ${ANT_HOME} && \
    #wget --no-check-certificate https://mirrors.tuna.tsinghua.edu.cn/apache/ant/binaries/apache-ant-${ANT_VERSION}-bin.tar.gz && \
    wget --no-check-certificate https://archive.apache.org/dist/ant/binaries/apache-ant-${ANT_VERSION}-bin.tar.gz && \
    tar -zvxf apache-ant-${ANT_VERSION}-bin.tar.gz -C ${ANT_HOME} --strip 1 && \
    rm -f apache-ant-${ANT_VERSION}-bin.tar.gz && \
    rm -f -R ${ANT_HOME}/manual/* && \
    cp $JMETER_HOME/extras/ant-jmeter-1.1.1.jar ${ANT_HOME}/lib/ant-jmeter-1.1.1.jar && \
    ln -s ${ANT_HOME}/bin/ant /usr/bin/ant && \
    rm -rf /tmp/* /var/cache/apk/*
    
RUN mkdir -p /home/jenkins/.m2/cicdrepository

ENV SONAR_SCANNER_OPTS="-Xmx512m"

COPY sonar-scanner-3.3.0.1492-linux /opt/sonar-scanner

RUN ln -s /opt/sonar-scanner/bin/sonar-scanner /usr/bin/sonar-scanner && \
    ln -s /opt/sonar-scanner/bin/sonar-scanner-debug /usr/bin/sonar-scanner-debug

ADD slave /slave

ENV S6_VERSION v1.22.1.0
RUN curl -o /tmp/s6-overlay-amd64.tar.gz -L https://github.com/just-containers/s6-overlay/releases/download/$S6_VERSION/s6-overlay-amd64.tar.gz && \
    tar xzf /tmp/s6-overlay-amd64.tar.gz -C / && \
    rm /tmp/s6-overlay-amd64.tar.gz && \
    mkdir /etc/services.d/jenkinsSlave/ && \
    echo "#!/usr/bin/with-contenv sh" >> /etc/services.d/jenkinsSlave/run && \
    echo "s6-svwait -t 5000 -u /var/run/s6/services/gossip" >> /etc/services.d/jenkinsSlave/run && \
    echo "exec jenkins-slave-dynamic.sh" >> /etc/services.d/jenkinsSlave/run && \
    mkdir /etc/services.d/gossip/ && \
    echo "#!/usr/bin/with-contenv sh" >> /etc/services.d/gossip/run && \
    echo 'exec /slave' >> /etc/services.d/gossip/run
    #echo 'exec /slave -gitlab_url=${GITLAB_URL} -gitlab_token=${GITLAB_PWD}' >> /etc/services.d/gossip/run

ENV S6_BEHAVIOUR_IF_STAGE2_FAILS 1

# Set up a standard volume for logs.
#VOLUME ["/var/log/services"]

ENV webhook=8081 \
    memberlist=7946
#webhook服务端口
EXPOSE ${webhook}
#memberlist监听端口
EXPOSE ${memberlist}

# 设置入口为 s6-based init.
ENTRYPOINT ["/init"]
