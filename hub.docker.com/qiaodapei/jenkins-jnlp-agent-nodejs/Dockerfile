FROM alpine:3.9
# 镜像的作者 
LABEL maintainer="<371583076@qq.com>" \
      name="jenkins" \
      author="xiao.li" \
      vendor="qiaodapei" \
      version="2.164.3" \
      systemver="alpine" \
      desc="alpine or nodejs" \
      build-date="20190510"   
COPY resource /tmp/resource
### SET ENVIRONNEMENT
ENV LANG=zh_CN.UTF-8 \
    LANGUAGE=zh_CN.UTF-8 \
    TIME_ZONE=Asia/Shanghai 
# Install language pack
RUN apk --no-cache add ca-certificates wget curl openjdk8  tzdata vim git openssh-client curl unzip bash ttf-dejavu coreutils tini nodejs npm yarn && \
    wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
    mkdir -p /data/jenkins_home  && mkdir -p /tmp/resource && cd /tmp/resource && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.25-r0/glibc-2.25-r0.apk && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.25-r0/glibc-bin-2.25-r0.apk && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.25-r0/glibc-i18n-2.25-r0.apk && \
    apk add glibc-bin-2.25-r0.apk glibc-i18n-2.25-r0.apk glibc-2.25-r0.apk && \
    npm install -g cnpm --registry=https://registry.npm.taobao.org && \
    cp -r /tmp/resource/agent.jar /usr/bin/agent.jar && \
    cp -r /tmp/resource/jenkins.sh /usr/local/bin/jenkins.sh && \
    chmod +x /usr/bin/agent.jar && chmod +x /usr/local/bin/jenkins.sh && \
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    rm -fr /tmp/resource 

WORKDIR /data/jenkins_home


ENTRYPOINT ["/sbin/tini", "--", "/usr/local/bin/jenkins.sh"]
