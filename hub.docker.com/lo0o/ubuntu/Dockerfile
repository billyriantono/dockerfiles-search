FROM ubuntu:16.04
MAINTAINER xiao-xing <xiao_xing@hansight.com>
RUN apt-get update
RUN apt-get install -y lsof man-db mtr nmap openssh-server strace traceroute
RUN apt-get install -y bind9-host curl wget dnsutils telnet tcpdump zlib1g-dev
RUN apt-get install -y gcc make
RUN apt-get install -y wget perl openssl libdbi1 libperl-dev sudo

# Prevent SSH from prompting about unknown hosts.

RUN echo 'UseDNS no' >> /etc/ssh/sshd_config
RUN echo 'UserKnownHostsFile /dev/null' >> /etc/ssh/ssh_config
RUN echo 'StrictHostKeyChecking no' >> /etc/ssh/ssh_config

# Allow login to playground servers via SSH, preventing (in auth.log):
#    Cannot open /proc/self/loginuid: Read-only file system
#    set_loginuid failed

RUN sed -i /loginuid/s/^/#/ /etc/pam.d/sshd

# Accept certificates signed by our own CA

ADD ca.crt /usr/local/share/ca-certificates/ca.crt
RUN update-ca-certificates

# Give users "root" and "lo0o" the password "abc123" on all hosts

RUN usermod -p '$6$sHTmsDVi$Spmhni61IjBGDsQBS/rYj1k4Do3u2HlI5qtCrPGn4mvqzogdagSjq0KqfeMXFpI2bqkg9OVOuZHEJOxtN.byy0' root
RUN useradd -d /home/lo0o -G sudo -m -p '$6$sHTmsDVi$Spmhni61IjBGDsQBS/rYj1k4Do3u2HlI5qtCrPGn4mvqzogdagSjq0KqfeMXFpI2bqkg9OVOuZHEJOxtN.byy0' -s /bin/bash lo0o

# Allow SSH login as root with a password.

RUN sed -i /PermitRootLogin/s/without-password/yes/ /etc/ssh/sshd_config

# Support SSH between hosts without a password.

RUN mkdir -p   /root/.ssh
ADD id_rsa     /root/.ssh/id_rsa
ADD id_rsa.pub /root/.ssh/id_rsa.pub
ADD id_rsa.pub /root/.ssh/authorized_keys
RUN chmod -R og-rwx /root/.ssh

# Allow "lo0o" to "sudo" without a password.

RUN sed -i '/sudo/s/ALL$/NOPASSWD: ALL/' /etc/sudoers

# Prevent a minor error message from filling /var/log/auth.log from SSH:
# "Unable to open env file: /etc/default/locale: No such file or directory"

RUN update-locale

RUN mkdir -p /home/lo0o/.ssh \
  && cp /root/.ssh/id_rsa /home/lo0o/.ssh/id_rsa \
  && cp /root/.ssh/id_rsa.pub  /home/lo0o/.ssh/id_rsa.pub \
  && cp /root/.ssh/authorized_keys /home/lo0o/.ssh/authorized_keys \
  && chown -R lo0o.lo0o /home/lo0o \
  && chmod -R og-rwx /home/lo0o/.ssh
