FROM centos:7

MAINTAINER zl1030 "zl1030@163.com"

RUN set -e \
    && yum update \
    && yum -y install java-1.8.0-openjdk maven openssh-clients

RUN java -version

RUN javac -version

RUN mvn -version

CMD ["/bin/bash"]
