FROM fedora

RUN dnf -y update && dnf -y install openssh-server passwd && dnf clean all

RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N '' \
     && sed -i 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config \
     && sed -i 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config \
     && sed -i 's/#PermitRootLogin yes/PermitRootLogin yes/' /etc/ssh/sshd_config \
     && mkdir -p /root/.ssh \
     && echo "StrictHostKeyChecking=no" > /root/.ssh/config \
     && echo "UserKnownHostsFile=/dev/null" >> /root/.ssh/config


RUN echo "root:fedora" | chpasswd

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]