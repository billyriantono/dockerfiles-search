FROM centos:centos6.6
#COPY \resources /tmp
RUN yum -y update
RUN useradd fuse
RUN yum -y install wget
RUN yum -y install unzip 
RUN yum -y install java-1.7.0-openjdk-devel
RUN yum -y install git
RUN yum -y install which
RUN yum -y install tar
RUN mkdir -m 777 -p /opt/fuse
#RUN unzip /tmp/jboss-fuse-full-6.2.0.redhat-133.zip -d /opt/fuse
#RUN sed -i '/#admin/s/^#//g' /opt/fuse/jboss-fuse-6.2.0.redhat-133/etc/users.properties
#RUN sed -i 's/root/fabric/g' /opt/fuse/jboss-fuse-6.2.0.redhat-133/etc/system.properties
#RUN echo 'bash /opt/fuse/jboss-fuse-6.2.0.redhat-133/bin/start' >> /root/.bashrc
