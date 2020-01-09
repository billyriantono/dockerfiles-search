# Pull base image.
FROM sherylynn/bash
MAINTAINER Sherylynn <352281674@qq.com>

# install openssl and the complete wget
RUN apk --update add --no-cache openssh openssh-sftp-server byobu tmux && \
    /bin/sed -i -e 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    /usr/bin/ssh-keygen -A && \
    echo "source /etc/profile.d/color_prompt" > /etc/skel/.bashrc && \
    cp /etc/skel/.bashrc /root/.bashrc && \
    echo "root:fuck" | chpasswd && \
    su - root -c "byobu-launcher-install"

# expose ports for ssh
EXPOSE 22
CMD    ["/usr/sbin/sshd", "-D", "-e"]