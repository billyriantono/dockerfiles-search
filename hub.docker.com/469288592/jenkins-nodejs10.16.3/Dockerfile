FROM centos:centos7.6.1810 
# 镜像的作者 
LABEL maintainer="<469288592@qq.com>" 

COPY resource /tmp/resource

ENV LANG=zh_CN.UTF-8 \
    LANGUAGE=zh_CN.UTF-8 \
    TIME_ZONE=Asia/Shanghai

RUN localedef -v -c -i en_US -f UTF-8 zh_CN.UTF-8 >/dev/null 2>&1 &&\
    grep -q 'zh_CN.utf8' /etc/locale.conf || sed -i -E 's/^LANG=.*/LANG="zh_CN.UTF-8"/' /etc/locale.conf &&\
    yum -y install http://rpms.famillecollet.com/enterprise/remi-release-7.rpm &&\
    yum install -y ntp yum-plugin-fastestmirror vim-enhanced ntp wget bash-completion elinks lrzsz unix2dos dos2unix git unzip net-tools cronie sudo tar &&\
    yum install -y rpm-build.x86_64 lua-devel libuv-devel sqlite-devel rpmdevtools mock &&\
    yum install -y java-1.8.0-openjdk java-1.8.0-openjdk-devel &&\
    yum -y install https://rpm.nodesource.com/pub_10.x/el/7/x86_64/nodejs-10.16.3-1nodesource.x86_64.rpm &&\
    npm install -g yarn &&\
    ###npm install -g cnpm --registry=https://registry.npm.taobao.org &&\
    rpmdev-setuptree &&\
    dos2unix /tmp/resource/*sh && \
    cp -r /tmp/resource/agent.jar /usr/bin/agent.jar && \
    cp -r /tmp/resource/jenkins.sh /usr/local/bin/jenkins.sh && \
    chmod +x /usr/bin/agent.jar && chmod +x /usr/local/bin/jenkins.sh && \
    mkdir -p /data/jenkins_home && \
    ln -nfs  /usr/share/zoneinfo/Asia/Shanghai /etc/localtime &&\
    yum clean all && rm -fr /tmp/resource


WORKDIR /data/jenkins_home

ENTRYPOINT ["/usr/local/bin/jenkins.sh"]

