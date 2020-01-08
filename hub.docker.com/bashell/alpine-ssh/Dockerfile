# ssh on alpine
#
# VERSION               0.0.2

FROM bashell/alpine-bash:latest
MAINTAINER Chaiwat Suttipongsakul "cwt@bashell.com"

# make sure the package repository is up to date
# then install dropbear as the sshd
RUN apk update && apk upgrade \
 && apk add openssh openssh-sftp-server byobu tmux \
 && rm -rf /var/cache/*/* \
 && /bin/sed -i -e 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
 && /bin/sed -i -e 's/#PermitUserEnvironment no/PermitUserEnvironment yes/' /etc/ssh/sshd_config \
 && mkdir -p /root/.ssh \
 && chmod 700 /root/.ssh \
 && /usr/bin/ssh-keygen -A \
 && echo "source /etc/profile.d/color_prompt" > /root/.bashrc \
 && echo "root:root" | chpasswd \
 && su - root -c "byobu-launcher-install"

ADD sshd.sh /

# expose ports for ssh
EXPOSE 22
CMD    ["/sshd.sh"]

