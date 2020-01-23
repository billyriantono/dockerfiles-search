FROM centos
MAINTAINER Charitra Maharjan charitra.maharjan1@gmail.com
#RUN mkdir /myvol
#RUN echo "echo world" >/myvol/greeting
#VOLUME /myvol
RUN yum -y install epel-release && \
    yum -y install nginx && \
    yum -y update 
#    yum clean all

COPY index.html /usr/share/nginx/html/
#ENV container docker
#RUN yum -y update; yum clean all
#RUN yum -y install systemd; yum clean all; \
#(cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
#rm -f /lib/systemd/system/multi-user.target.wants/*;\
#rm -f /etc/systemd/system/*.wants/*;\
#rm -f /lib/systemd/system/local-fs.target.wants/*; \
#rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
#rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
#rm -f /lib/systemd/system/basic.target.wants/*;\
#rm -f /lib/systemd/system/anaconda.target.wants/*;
#VOLUME [ “/sys/fs/cgroup” ]
#CMD [“/usr/sbin/init”]

#RUN systemctl enable nginx && \
#    systemctl start nginx
#EXPOSE 80
