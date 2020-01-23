FROM centos:7
MAINTAINER zzn <zineng.zhao@implustech.com>

ENV JAVA_VERSION "8u172"
ENV BUILD_VERSION "b15"
ENV JDK_VERSION "1.8.0_172"

RUN yum update && yum install -y wget curl \
    && mkdir -p /usr/lib/jvm \
    && cd /usr/lib/jvm \
    #&& wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION}-${BUILD_VERSION}/server-jre-${JAVA_VERSION}-linux-x64.tar.gz" \
    && wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u172-b11/a58eab1ec242421181065cdc37240b08/jre-8u172-linux-x64.tar.gz" \
    && tar -zxvf jre-${JAVA_VERSION}-linux-x64.tar.gz \
    && rm /usr/lib/jvm/jre-${JAVA_VERSION}-linux-x64.tar.gz \
    && ln -s /usr/lib/jvm/jre${JDK_VERSION}/bin/java /bin/ \
    && cd /usr/lib/jvm/jre${JDK_VERSION} \
    && find . -type f -name '*.html' -delete \
    && find . -type f -name '*.bat' -delete \
    && find . -type f -name 'COPYRIGHT' -delete \
    && find . -type f -name 'LICENSE' -delete \
    && find . -type f -name 'NOTICE' -delete \
    && find . -type f -name '3RDPARTY' -delete \
    && find . -type f -name 'THIRDPARTYLICENSE.txt' -delete \
    && yum clean all\
    && rm -rf /var/cache/yum
