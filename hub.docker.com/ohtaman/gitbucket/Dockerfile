FROM centos

MAINTAINER ohtaman

RUN yum -y update
RUN yum -y install java-1.8.0-openjdk
RUN yum clean all

ADD https://github.com/takezoe/gitbucket/releases/download/4.8/gitbucket.war /opt/gitbucket/gitbucket.war

RUN ln -s /gitbucket /root/.gitbucket

VOLUME /gitbucket
EXPOSE 8080

CMD ["java", "-jar", "/opt/gitbucket/gitbucket.war"]
