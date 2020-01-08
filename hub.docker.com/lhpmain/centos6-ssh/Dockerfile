#Dockerfile
FROM scratch
MAINTAINER lhpmain "lhpmain@126.com"    # lhpmain-mail
ADD centos-68-docker.tar.xz /
#ADD https://raw.githubusercontent.com/lhpmain/sig-cloud-instance-images/CentOS-6.10/docker/centos-6-docker.tar.xz /
LABEL name="CentOS Base Image" \
    vendor="CentOS" \
    license="GPLv2" \
    build-date="20181204"
    
CMD ["/bin/bash"]

#update yum repository and install openssh server
RUN yum install wget -y 
#RUN yum update -y
RUN yum install -y openssh-server
#RUN service iptables stop
#RUN chkconfig iptables off

#generate ssh key
RUN ssh-keygen -q -N "" -t dsa -f /etc/ssh/ssh_host_dsa_key
RUN ssh-keygen -q -N "" -t rsa -f /etc/ssh/ssh_host_rsa_key
RUN sed -ri 's/session    required     pam_loginuid.so/#session    required     pam_loginuid.so/g' /etc/pam.d/sshd
RUN mkdir -p /root/.ssh && chown root.root /root && chmod 700 /root/.ssh

#change root password to 123456
RUN echo 'root:123456' | chpasswd

#RUN curl https://git.oschina.net/feedao/Docker_shell/raw/start/ali-centos.sh | sh
#ENV LANG en_US.UTF-8
#ENV LC_ALL en_US.UTF-8

# install ipsec
#RUN curl https://raw.githubusercontent.com/lhpmain/setup-ipsec-vpn/master/vpnsetup_centos.sh -O vpnsetup.sh && sudo sh vpnsetup.sh | sh
RUN wget -N --no-check-certificate https://raw.githubusercontent.com/lhpmain/doubi1/master/ssrmu.sh && chmod +x ssrmu.sh && bash ssrmu.sh

#RUN reboot

#g
ADD kernel-2.6.32-504.3.3.el6.x86_64.rpm /
RUN yum install -y kernel-2.6.32-504.3.3.el6.x86_64.rpm
RUN rpm -e kernel-firmware-2.6.32-754.18.2.el6.noarch
RUN rpm -e dracut-kernel-004-411.el6.noarch


EXPOSE 22
CMD /usr/sbin/sshd -D
#End
