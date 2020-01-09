FROM centos:latest

WORKDIR /tmp/

RUN curl https://www.centos.org/keys/RPM-GPG-KEY-CentOS-7 --output RPM-GPG-KEY-CentOS-7
RUN rpm --import RPM-GPG-KEY-CentOS-7
RUN yum update -y
RUN yum -y install java-1.8.0-openjdk

# Clean up yum and tmp
RUN yum clean all
RUN rm -rf /tmp/
RUN rm -rf /var/cache/yum 

WORKDIR /opt/
RUN curl -L http://download.sonatype.com/nexus/3/nexus-3.14.0-04-unix.tar.gz --output nexus-3.14.0-04-unix.tar.gz 
RUN tar xvf nexus-3.14.0-04-unix.tar.gz

# Clean nexus archive
RUN rm -f nexus-3.14.0-04-unix.tar.gz

RUN useradd nexus
RUN chown nexus:root -R /opt/nexus-3.14.0-04/
RUN chown nexus:root -R /opt/sonatype-work/

WORKDIR /opt/nexus-3.14.0-04/bin/

USER nexus
ENTRYPOINT [ "./nexus", "run" ]

VOLUME [ "/opt/sonatype-work/" ]

EXPOSE 8081
EXPOSE 8443
