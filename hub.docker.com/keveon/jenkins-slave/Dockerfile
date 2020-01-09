FROM maven:alpine
LABEL maintainer="keveon <keveon@keveon.com>"

ARG VERSION=3.35
ARG user=jenkins
ARG group=jenkins
ARG uid=1000
ARG gid=1000

## Container environment variables
ENV LANG C.UTF-8
ENV TZ=Asia/Shanghai
ENV JAVA_OPTS=" -XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap -XX:MaxRAMFraction=1 -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=${dumpdr:-/root} -Xloggc:${dumpdr:-/root}/gc.log -XX:+PrintGCTimeStamps -Dfile.encoding=utf-8 -Dsun.jnu.encoding=utf-8 -Duser.timezone=${TZ} -Djava.security.egd=file:/dev/./urandom"
ENV MAVEN_OPTS=" -Dorg.slf4j.simpleLogger.log.org.apache.maven.cli.transfer.Slf4jMavenTransferListener=WARN -Dorg.slf4j.simpleLogger.showDateTime=true -Djava.awt.headless=true "
ENV MAVEN_CLI_OPTS=" --batch-mode --errors --fail-at-end --show-version -Dfile.encoding=UTF-8 -Ddisable.git-hooks -Dsonar.sourceEncoding=UTF-8 -Dsonar.host.url=http://sonar.thunisoft.com -Dsonar.login=1193ca99634421e6656f2444de264d65ec9988e9 "

## Create User
RUN addgroup -g ${gid} ${group}
RUN adduser -h /home/${user} -u ${uid} -G ${group} -D ${user}

## Install requirements
RUN apk add --update --no-cache \
        bash \
        procps \
        git git-lfs \
        curl wget \
        tar gzip \
        openssl openssh-client ca-certificates \
        nodejs npm yarn \
        tzdata && \
    \
    ## TZ Data
    cp /usr/share/zoneinfo/${TZ} /etc/localtime && \
    echo ${TZ} > /etc/timezone && \
    rm -f /var/cache/apk/*

## Configuration Maven Mirrors
COPY usr/share/maven/conf /usr/share/maven/conf

## Configuration Nodejs
RUN npm config set registry https://registry.npm.taobao.org/ && \
    npm config set electron_mirror https://npm.taobao.org/mirrors/electron/ && \
    npm config set phantomjs_cdnurl https://npm.taobao.org/mirrors/phantomjs/ && \
    npm config set chromedriver_cdnurl https://npm.taobao.org/mirrors/chromedriver/ && \
    npm config set sass_binary_site https://npm.taobao.org/mirrors/node-sass/ && \
    yarn config set registry https://registry.npm.taobao.org/ && \
    node -v && npm -v && yarn -v

## Install glibc
RUN version=2.30-r0 && \
    wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${version}/glibc-${version}.apk && \
    apk add --no-cache glibc-${version}.apk && \
    rm glibc-${version}.apk && \
    rm -rf /var/cache/apk/* \
    unset version

## Install Kubernetes Helm
RUN curl -L https://get.helm.sh/helm-v3.0.0-linux-amd64.tar.gz | tar xvz && \
    mv linux-amd64/helm /usr/bin/helm && \
    chmod +x /usr/bin/helm && \
    rm -rf linux-amd64 && \
    rm -f /var/cache/apk/* && \
    helm version --client

## Install kubectl
RUN BASE_URL="https://storage.googleapis.com/kubernetes-release/release" && \
    curl -L -o /usr/bin/kubectl ${BASE_URL}/$(curl -s ${BASE_URL}/latest.txt)/bin/linux/amd64/kubectl && \
    chmod +x /usr/bin/kubectl && \
    kubectl version --client \
    unset BASE_URL

## Install Minio Client
RUN curl https://dl.min.io/client/mc/release/linux-amd64/mc > /usr/bin/mc && \
    chmod +x /usr/bin/mc && \
    mc version

## Install Jenkins Slave
ARG AGENT_WORKDIR=/home/${user}/agent

COPY jenkins /usr/bin/jenkins

RUN curl --create-dirs -fsSLo \
        /usr/share/jenkins/agent.jar \
        https://repo.jenkins-ci.org/public/org/jenkins-ci/main/remoting/${VERSION}/remoting-${VERSION}.jar \
  && chmod 755 /usr/share/jenkins \
  && chmod 644 /usr/share/jenkins/agent.jar \
  && ln -sf /usr/share/jenkins/agent.jar /usr/share/jenkins/slave.jar \
  && chmod +x /usr/bin/jenkins

# USER ${user}
ENV AGENT_WORKDIR=${AGENT_WORKDIR}
RUN mkdir -p /home/${user}/.jenkins && mkdir -p ${AGENT_WORKDIR}

VOLUME /home/${user}/.jenkins
VOLUME ${AGENT_WORKDIR}
WORKDIR /home/${user}

ENTRYPOINT ["/usr/bin/jenkins"]
