FROM centos:centos7.7.1908
MAINTAINER "kongfanhong@docker.com"
# centos:centos7.7.1908, jre-8u211 

### timezone
RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' > /etc/timezone

ENV LANG="en_US.UTF-8" \
    LANGUAGE="en_US:en" \
    LC_ALL="en_US.UTF-8"

ENV JAVA_VERSION="1.8.0_211"

### install jre
ADD jre-8u211-linux-x64.tar.gz /usr/local/

ENV JAVA_HOME="/usr/local/jre${JAVA_VERSION}"
ENV PATH="$JAVA_HOME/bin:$PATH"

ENV JAVA_OPTS="-Dspring.profiles.active=default"

 
