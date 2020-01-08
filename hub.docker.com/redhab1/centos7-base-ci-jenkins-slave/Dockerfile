#########################################
# Name: redhab1/centos7-base-ci-jenkins-slave
# Description: Centos7 based Continuous Integration Jenkins Slave image
#
# Includes:
#  - JDK-1.8.121_b13
#  - Maven 3.3.9
#  - Git: latest
#  - SSH Server
#  - Jenkins user with sudo access
#
# To build image:
#    docker build -t redhab1/centos7-base-ci-jenkins-slave .
#
# To run container:
#    docker run -d -t -i -p 2222:22 redhab1/centos7-base-ci-jenkins-slave
#
# Change Log:
#  03/18/17: Initial version
#########################################
FROM centos:centos7

LABEL name="redhab1/centos7-base-ci-jenkins-slave"
LABEL description="Centos7 based Continuous Integration Jenkins Slave image"
LABEL maintainer="Redha Boukefoussa redhab@gmail.com"

ENV JAVA_VERSION=8 \
    JAVA_UPDATE=121 \
    JAVA_BUILD=13 \
    JAVA_PATH=e9e7ea248e2c4826b92b3f075a80e441 \
    \
    MAVEN_VERSION=3.3.9

ENV JAVA_RPM="jdk-${JAVA_VERSION}u${JAVA_UPDATE}-linux-x64.rpm"
ENV JAVA_RPM_URL="http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION}u${JAVA_UPDATE}-b${JAVA_BUILD}/${JAVA_PATH}/${JAVA_RPM}"

ENV MAVEN_PCK="apache-maven-${MAVEN_VERSION}-bin.tar.gz"
ENV MAVEN_PCK_URL="http://mirror.cogentco.com/pub/apache/maven/maven-3/${MAVEN_VERSION}/binaries/${MAVEN_PCK}"

RUN echo "- Install wget - unzip - git - sudo - SSH Server" \
    && yum -y install \
       wget \
       unzip \
       git \
       sudo \
       openssh-server \
    \
    \
    && echo "- Download Oracle JDK" \
    && echo "  - URL: ${JAVA_RPM_URL}" \
    && wget --quiet \
         -O /tmp/${JAVA_RPM} \
         --no-check-certificate \
         --no-cookies \
         --header "Cookie: oraclelicense=accept-securebackup-cookie" \
         ${JAVA_RPM_URL} \
    \
    && echo "- Install Oracle: JDK $JAVA_RPM" \
    && yum localinstall -y \
           /tmp/${JAVA_RPM} \
    \
    \
    && echo "- Download Apache Maven ${MAVEN_VERSION}" \
    && wget --no-verbose \
         -O /tmp/${MAVEN_PCK} \
         ${MAVEN_PCK_URL} \
    \
    \
    && echo "- Install Apache Maven ${MAVEN_VERSION}" \
    && sudo tar xzf /tmp/${MAVEN_PCK} \
         -C /opt/ \
    && sudo ln -s /opt/apache-maven-${MAVEN_VERSION} /opt/maven \
    && sudo ln -s /opt/maven/bin/mvn /usr/local/bin \
    \
    \
    && echo "- Configure SSH Server" \
    && /usr/bin/ssh-keygen -A \ 
    && sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd   \
    && rm -f /etc/ssh/ssh_host_rsa_key \
    && ssh-keygen -q -N '' -t rsa -f /etc/ssh/ssh_host_rsa_key  \
    && rm -f /etc/ssh/ssh_host_ecdsa_key \
    && ssh-keygen -q -N '' -t dsa -f /etc/ssh/ssh_host_ecdsa_key  \
    && mkdir -p /var/run/sshd \
    \
    \
    && echo "- Add Jenkins user" \
    && useradd -m -d /home/jenkins jenkins \
    && echo "jenkins:jenkins" | chpasswd \
    && mkdir -p /home/jenkins/.ssh \
    && chmod 700 /home/jenkins/.ssh \
    && echo "jenkins   ALL=(ALL)       NOPASSWD: ALL" >> /etc/sudoers \
    \
    \
    && echo "- Clean up" \
    && yum clean all \
    && rm -rf \
          /tmp/* \
          /var/tmp/*

# set the Java environment variables
ENV JAVA_HOME=/usr/java/latest \
    MAVEN_HOME=/opt/maven

ENV PATH=${PATH}:${JAVA_HOME}/jre/bin:${MAVEN_HOME}/bin

LABEL java.version="JDK 1.${JAVA_VERSION}.${JAVA_UPDATE}_${JAVA_BUILD}"
LABEL maven.version="${MAVEN_VERSION}"
LABEL git.version="latest"

# Standard SSH port
EXPOSE 22

# Default command
CMD ["/usr/sbin/sshd", "-D"]