FROM centos:7
MAINTAINER dotNetDR_ <dotnetdr1987@gmail.com>

# beijing china yum source very fast...(in china [gfw], you know 0.0)
COPY yun-idc.repo /yun-idc.repo
COPY runssh.sh /runssh.sh

RUN rm -rf /etc/yum.repos.d/*.repo && \
  mv /yun-idc.repo /etc/yum.repos.d/yun-idc.repo && \
  yum clean all && \
  yum install -y openssh-server && \
  touch /etc/rc.d/init.d/functions && \
  /usr/sbin/sshd-keygen && \
  chmod +x /runssh.sh
  
EXPOSE 22
ENTRYPOINT ["/runssh.sh"]
CMD ["123456"]
