# For fedora20

FROM fedora:20
MAINTAINER Quey-Liang Kao <s101062801@m101.nthu.edu.tw>
# Last Modified: 2015/2/2

RUN yum -y install wget vim
RUN wget http://ftp.yzu.edu.tw/Linux/Fedora-EPEL/7/x86_64/e/epel-release-7-5.noarch.rpm
RUN yum -y install epel-release-7-5.noarch.rpm
RUN yum -y install openssh openssh-clients openssh-server
RUN echo 'root:sshtest' | chpasswd
RUN sed -i 's/UsePrivilegeSeparation\(.*\)sandbox/UsePrivilegeSeparation no/' /etc/ssh/sshd_config
RUN sed -i 's/#StrictModes yes/StrictModes no/' /etc/ssh/sshd_config
RUN sed -i 's/.*UseDNS yes/UseDNS no/' /etc/ssh/sshd_config
RUN sed -i 's/GSSAPIAuthentication yes/GSSAPIAuthentication no/' /etc/ssh/sshd_config
RUN sed -i 's/.*StrictHostKeyChecking.*/StrictHostKeyChecking no/' /etc/ssh/ssh_config
# disable prompt for first-time login
RUN sed -i 's/required     pam_loginuid.so/optional     pam_loginuid.so/' /etc/pam.d/sshd
# fedora does NOT permit disabling PAM 
# make pam_loginuid module less restricted
RUN ssh-keygen -A
#RUN mkdir /root/.ssh/
#ADD id_rsa /root/.ssh/
#ADD id_rsa.pub /root/.ssh/
#ADD authorized_keys /root/.ssh/

EXPOSE 22
ENTRYPOINT ["/usr/sbin/sshd"]
CMD ["-D"]

