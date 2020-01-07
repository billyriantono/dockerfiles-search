FROM centos:centos7
MAINTAINER hqli@freewheel.tv

RUN yum -y groups install "Development Tools" && yum -y install maven java-1.7.0-openjdk openssh-server && yum -y clean all

# Config SSH and Permit Root Login
RUN mkdir -p /var/run/sshd
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N ''
RUN sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd
RUN sed -i 's|HostKey /etc/ssh/ssh_host_ecdsa_key|#HostKey /etc/ssh/ssh_host_ecdsa_key|g' /etc/ssh/sshd_config
RUN sed -i 's|HostKey /etc/ssh/ssh_host_ed25519_key|#HostKey /etc/ssh/ssh_host_ed25519_key|g' /etc/ssh/sshd_config
RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config
RUN echo "root:root" | chpasswd

# Set JAVA HOME
RUN echo "JAVA_HOME=/etc/alternatives/java_sdk_openjdk" > /etc/profile.d/java.sh
ENV JAVA_HOME /etc/alternatives/java_sdk_openjdk

# Standard SSH port
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
