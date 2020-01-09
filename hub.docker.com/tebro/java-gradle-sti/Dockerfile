FROM openshift/base-centos7
MAINTAINER Richard Weber <riche.weber@gmail.com>

LABEL io.k8s.description="Java with JDK" \
    io.openshift.tags="builder,java,jdk" \
    io.openshift.s2i.scripts-url="image:///usr/libexec/s2i"

RUN yum install -y java-1.8.0-openjdk-devel
RUN yum clean all

COPY ["run", "assemble", "/usr/libexec/s2i/"]
RUN chmod +x /usr/libexec/s2i/*

RUN chmod -R 777 /opt

USER 1001
