# alpine-byobu-ssh

FROM samxzxy/alpine-base:3.4
MAINTAINER Sam ccopsuse#g!.com

RUN apk update && apk upgrade && apk add --update --no-cache openssh openssh-sftp-server byobu tmux

RUN /bin/sed -i -e 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    /usr/bin/ssh-keygen -A && \
    echo "source /etc/profile.d/color_prompt" > /etc/skel/.bashrc && \
    cp /etc/skel/.bashrc /root/.bashrc && \
    echo "root:root" | chpasswd && \
    su - root -c "byobu-launcher-install" && \
    rm -rf /var/cache/apk/*

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D", "-e"]
