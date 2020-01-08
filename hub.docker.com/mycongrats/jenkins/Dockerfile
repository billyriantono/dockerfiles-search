FROM centos:7

RUN cd ~ \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && curl -O -L "http://mirrors.jenkins.io/war-stable/latest/jenkins.war" \
    && curl -O -H "Cookie: oraclelicense=accept-securebackup-cookie" -H "Connection: keep-alive" -L "https://download.oracle.com/otn-pub/java/jdk/8u201-b09/42970487e3af4f5aa5bca3f542482c60/jre-8u201-linux-x64.rpm" \
    && yum install ./jre-8u201-linux-x64.rpm -y \
    && yum clean all \
    && rm -rf ./jre-8u201-linux-x64.rpm

ENV JENKINS_HOME /var/lib/jenkins

CMD ["java", "-jar", "/root/jenkins.war"]
