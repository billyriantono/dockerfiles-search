FROM centos:centos7.6.1810
# 镜像的作者
LABEL maintainer="<371583076@qq.com>" \
      name="jenkins" \
      author="xiao.li" \
      vendor="qiaodapei" \
      version="2.190.3" \
      systemver="centos" \
      desc="centos or jenkins" \
      build-date="201901206"

ARG user=jenkins
ARG group=jenkins
ARG uid=1000
ARG gid=1000
ARG http_port=8080
ARG agent_port=50000
ARG JENKINS_HOME=/var/jenkins_home
ARG TINI_VERSION=v0.16.1
ARG JENKINS_VERSION=2.190.3
ARG JENKINS_SHA=79c2042b30ad71dc9cf17a5877f64eaed405fa03e24e002ca60f8db73b7ad490
ARG JENKINS_URL=https://repo.jenkins-ci.org/public/org/jenkins-ci/main/jenkins-war/${JENKINS_VERSION}/jenkins-war-${JENKINS_VERSION}.war

### SET ENVIRONNEMENT
ENV LANG=zh_CN.UTF-8 \
    LANGUAGE=zh_CN.UTF-8 \
    TIME_ZONE=Asia/Shanghai \
    JENKINS_HOME=$JENKINS_HOME \
    JENKINS_SLAVE_AGENT_PORT=${agent_port} \
    JENKINS_VERSION=${JENKINS_VERSION:-2.121.1} \
    JENKINS_UC=https://updates.jenkins.io \
    JENKINS_UC_EXPERIMENTAL=https://updates.jenkins.io/experimental \
    JENKINS_INCREMENTALS_REPO_MIRROR=https://repo.jenkins-ci.org/incrementals \
    COPY_REFERENCE_FILE_LOG=$JENKINS_HOME/copy_reference_file.log \
    JENKINS_BACKUP=/data/jenkins_backup


COPY Resource /tmp/Resource
RUN localedef -v -c -i en_US -f UTF-8 zh_CN.UTF-8 >/dev/null 2>&1 &&\
    ln -nfs  /usr/share/zoneinfo/Asia/Shanghai /etc/localtime &&\
    grep -q 'zh_CN.utf8' /etc/locale.conf || sed -i -E 's/^LANG=.*/LANG="zh_CN.UTF-8"/' /etc/locale.conf &&\
    yum -y install http://rpms.famillecollet.com/enterprise/remi-release-7.rpm &&\
    yum install -y ntp yum-plugin-fastestmirror vim-enhanced ntp wget bash-completion elinks lrzsz unix2dos dos2unix git curl unzip net-tools cronie java-1.8.0-openjdk &&\
    mkdir -p $JENKINS_HOME && chown ${uid}:${gid} $JENKINS_HOME && groupadd -g ${gid} ${group} && useradd -d "$JENKINS_HOME" -u ${uid} -g ${gid} -m -s /bin/bash ${user} &&\
    mkdir -p /usr/share/jenkins/ref/init.groovy.d && cp -r /tmp/Resource/tini_pub.gpg  ${JENKINS_HOME}/tini_pub.gpg &&\
    curl -fsSL https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini-static-amd64 -o /sbin/tini &&\
    curl -fsSL https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini-static-amd64.asc -o /sbin/tini.asc &&\
    gpg --no-tty --import ${JENKINS_HOME}/tini_pub.gpg && gpg --verify /sbin/tini.asc && rm -rf /sbin/tini.asc /root/.gnupg && chmod +x /sbin/tini &&\
    curl -fsSL ${JENKINS_URL} -o /usr/share/jenkins/jenkins.war && echo "${JENKINS_SHA}  /usr/share/jenkins/jenkins.war" | sha256sum -c - &&\
    chown -R ${user} "$JENKINS_HOME" /usr/share/jenkins/ref && cp -r /tmp/Resource/jenkins-support /usr/local/bin/jenkins-support &&\
    cp -r /tmp/Resource/jenkins.sh /usr/local/bin/jenkins.sh && cp -r /tmp/Resource/jenkins.sh /usr/local/bin/jenkins.sh &&\
    cp -r /tmp/Resource/tini-shim.sh /bin/tini && cp -r /tmp/Resource/plugins.sh /usr/local/bin/plugins.sh && \
    cp -r /tmp/Resource/install-plugins.sh /usr/local/bin/install-plugins.sh && \
    mkdir -p ${JENKINS_BACKUP} && yum clean all && rm -fr /tmp/Resources

WORKDIR $JENKINS_HOME
VOLUME  ["$JENKINS_HOME","${JENKINS_BACKUP}"]
EXPOSE ${http_port}/tcp ${agent_port}/tcp

USER ${user}
ENTRYPOINT ["/sbin/tini", "--", "/usr/local/bin/jenkins.sh"]
