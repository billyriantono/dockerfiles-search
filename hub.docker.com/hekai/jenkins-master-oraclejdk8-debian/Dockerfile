FROM jenkins/jenkins:lts

LABEL maintainer="hekai <hekai@aisino.com>"

USER root

# oracle jdk 必须登录才能下载，所以在构建时传入自己建立的jdk下载地址
ARG JDK_DOWNLOAD_URL

ENV TZ="Aisa/Shanghai" \
    LC_ALL=zh_CN.UTF-8 \
    LANG=zh_CN.UTF-8 \
    LANGUAGE=zh_CN:zh \
    KUBECTL_VERSION=v1.15.0 \
    MAVEN_VERSION=3.6.2 \
    MAVEN_HOME=/usr/local/maven \
    JAVA_VERSION=8u231 \
    JAVA_HOME=/usr/local/jdk

# 重新定义path，从而去除openjdk的path
ENV PATH ${MAVEN_HOME}/bin:${JAVA_HOME}/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

ENV KUBERNETES_CLIENT_DOWNLOAD_URL https://dl.k8s.io/${KUBECTL_VERSION}/kubernetes-client-linux-amd64.tar.gz
ENV MAVEN_DOWNLOAD_URL http://mirrors.tuna.tsinghua.edu.cn/apache/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz

COPY settings.xml /tmp/

RUN set -ex &&\
    echo "deb http://mirrors.aliyun.com/debian/ stretch main non-free contrib" > /etc/apt/sources.list &&\
    echo "deb http://mirrors.aliyun.com/debian-security stretch/updates main" >> /etc/apt/sources.list &&\
    echo "deb http://mirrors.aliyun.com/debian/ stretch-updates main non-free contrib" >> /etc/apt/sources.list &&\
    echo "deb http://mirrors.aliyun.com/debian/ stretch-backports main non-free contrib" >> /etc/apt/sources.list &&\
    # Update and install libltdl7
    apt update && apt install -y apt-utils libltdl7 locales &&\
    # download and install kubectl
    wget ${KUBERNETES_CLIENT_DOWNLOAD_URL} -O /tmp/client.tar.gz &&\
    tar -zxvf /tmp/client.tar.gz  --strip-components=3 -C /usr/local/bin kubernetes/client/bin/kubectl &&\
    chmod +x /usr/local/bin/kubectl &&\
    # unistall openjdk, dockerfile of openjdk: https://github.com/docker-library/openjdk/blob/master/8/jdk/Dockerfile
    rm -rf /usr/local/openjdk* \
           /etc/ca-certificates/update.d/docker-openjdk &&\
    # install oracle jdk
    wget ${JDK_DOWNLOAD_URL} -O /tmp/jdk.tar.gz &&\
    mkdir -p ${JAVA_HOME} &&\
    tar -zxvf /tmp/jdk.tar.gz --strip-components=1 -C ${JAVA_HOME} &&\
    # download and install maven
    wget ${MAVEN_DOWNLOAD_URL} -O /tmp/maven.tar.gz &&\
    mkdir -p ${MAVEN_HOME} &&\
    tar -zxvf /tmp/maven.tar.gz --strip-components=1 -C ${MAVEN_HOME} &&\
    mv /tmp/settings.xml ${MAVEN_HOME}/conf/settings.xml &&\
    # support zh_CN.UTF-8
    locale-gen --purge zh_CN.UTF-8 &&\
    localedef -i zh_CN -c -f UTF-8 zh_CN.UTF-8 &&\
    echo 'LANG="zh_CN.UTF-8"' > /etc/default/locale &&\
    echo 'LANGUAGE="zh_CN.UTF-8"' >> /etc/default/locale &&\
    # change timezone to Aisa/Shanghai
    ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime &&\
    echo "${TZ}" > /etc/timezone &&\
    cd /usr/share/i18n/charmaps &&\
    ls|egrep -v 'UTF-8.gz|GB18030.gz|GBK.gz|GB2312.gz|ISO-8859-1.gz'|xargs rm -rf &&\
    cd /usr/share/i18n/locales &&\
    ls|egrep -v 'zh_CN'|xargs rm -rf &&\
    echo 'zh_CN.UTF-8 UTF-8\nzh_CN.GB18030 GB18030\nzh_CN.GBK GBK\nzh_CN GB2312' > /usr/share/i18n/SUPPORTED &&\
    apt autoremove -y &&\
    rm -rf  /var/lib/apt/lists/* \
            /var/log/* \
            /var/cache/* \
            /tmp/* \
            ${JAVA_HOME}/*src.zip \
            ${JAVA_HOME}/man \
            ${JAVA_HOME}/*.txt \
            ${JAVA_HOME}/*.html \
            ${JAVA_HOME}/COPYRIGHT \
            ${JAVA_HOME}/LICENSE \
            ${JAVA_HOME}/release \
            ${JAVA_HOME}/bin/jmc* \
            ${JAVA_HOME}/bin/jvisualvm \
            ${JAVA_HOME}/bin/*javafx* \
            ${JAVA_HOME}/bin/appletviewer \
            ${JAVA_HOME}/bin/javapackager \
            ${JAVA_HOME}/bin/jconsole \
            ${JAVA_HOME}/bin/ControlPanel \
            ${JAVA_HOME}/bin/jcontrol \
            ${JAVA_HOME}/lib/missioncontrol \
            ${JAVA_HOME}/lib/visualvm \
            ${JAVA_HOME}/lib/*javafx* \
            ${JAVA_HOME}/lib/jconsole.jar \
            ${JAVA_HOME}/lib/packager.jar \
            ${JAVA_HOME}/jre/*.txt \
            ${JAVA_HOME}/jre/*.html \
            ${JAVA_HOME}/jre/COPYRIGHT \
            ${JAVA_HOME}/jre/LICENSE \
            ${JAVA_HOME}/jre/README \
            ${JAVA_HOME}/jre/plugin \
            ${JAVA_HOME}/jre/bin/ControlPanel \
            ${JAVA_HOME}/jre/bin/jcontrol \
            ${JAVA_HOME}/jre/lib/deploy* \
            ${JAVA_HOME}/jre/lib/desktop \
            ${JAVA_HOME}/jre/lib/*javafx* \
            ${JAVA_HOME}/jre/lib/*jfx* \
            ${JAVA_HOME}/jre/lib/oblique-fonts \
            ${JAVA_HOME}/jre/lib/plugin.jar \
            ${JAVA_HOME}/jre/lib/amd64/libavplugin*.so \
            ${JAVA_HOME}/jre/lib/amd64/libde*.so \
            ${JAVA_HOME}/jre/lib/amd64/libfxplugins.so \
            ${JAVA_HOME}/jre/lib/amd64/libgl*.so \
            ${JAVA_HOME}/jre/lib/amd64/libgstreamer-lite.so \
            ${JAVA_HOME}/jre/lib/amd64/libjavafx*.so \
            ${JAVA_HOME}/jre/lib/amd64/libjfx*.so \
            ${JAVA_HOME}/jre/lib/amd64/libnpjp2.so \
            ${JAVA_HOME}/jre/lib/amd64/libprism_*.so \
            ${JAVA_HOME}/jre/lib/amd64/libfxplugins.so \
            ${JAVA_HOME}/jre/lib/amd64/server/libjsig.so \
            ${JAVA_HOME}/jre/lib/deploy \
            ${JAVA_HOME}/jre/lib/images/icons \
            ${JAVA_HOME}/jre/lib/locale \
            ${JAVA_HOME}/jre/lib/ext/jfxrt.jar \
            ${JAVA_HOME}/jre/lib/ext/jaccess.jar &&\
    ln -s ${JAVA_HOME}/jre/lib/amd64/libjsig.so ${JAVA_HOME}/jre/lib/amd64/server/libjsig.so
