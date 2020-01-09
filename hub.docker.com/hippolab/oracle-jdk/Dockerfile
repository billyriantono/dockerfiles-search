FROM centos

ARG JAVA_URL="https://download.oracle.com/otn-pub/java/jdk/8u191-b12/2787e4a523244c269598db4e85c51e0c/jdk-8u191-linux-x64.tar.gz"

ENV JAVA_HOME=/opt/oracle-jdk

WORKDIR /opt/oracle-jdk

RUN curl -sL -H 'Cookie: oraclelicense=accept-securebackup-cookie' ${JAVA_URL} | tar --strip=1 -xz && \
    for i in $(find /opt/oracle-jdk -type f -executable); do ln -sv ${i} /usr/bin/; done && \
    echo "export JAVA_HOME=${JAVA_HOME}" > /etc/profile.d/oracle-jdk.sh
