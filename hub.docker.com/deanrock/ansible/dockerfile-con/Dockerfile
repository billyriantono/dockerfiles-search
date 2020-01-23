FROM centos
MAINTAINER de13 <stephane.beuret@data-essential.com>
RUN yum update -y && yum install -y xauth firefox openssh-server && \
    od -N32 -x < /dev/urandom | head -n1 |  cut -b9- | sed 's/ //gi' > /etc/machine-id && \
    sed  -i '/#PermitR./ {s/#//}' /etc/ssh/sshd_config && \
    /usr/bin/ssh-keygen -t rsa -P '' -f /etc/ssh/ssh_host_rsa_key && \
    /usr/bin/ssh-keygen -t ecdsa -P '' -f /etc/ssh/ssh_host_ecdsa_key && \
    /usr/bin/ssh-keygen -t ed25519 -P '' -f /etc/ssh/ssh_host_ed25519_key && \
    echo password | passwd --stdin root
EXPOSE 22
CMD [ "/usr/sbin/sshd", "-D" ]
