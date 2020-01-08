FROM ubuntu:12.04

RUN apt-get -q -y update
RUN echo "deb http://us.archive.ubuntu.com/ubuntu/ precise universe" >> /etc/apt/sources.list
RUN apt-get -q -y update
RUN apt-get install -q -y wget curl build-essential git screen tmux python-software-properties openssl whois openssh-server vim nano htop expect

RUN rm -Rf /root/.vim

RUN cd /root/ && git clone https://github.com/thestonefox/vim-config.git
RUN mv /root/vim-config/.vim /root/
RUN mv /root/vim-config/.vimrc /root/
RUN rm -Rf /root/vim-config

RUN curl -Sso /root/.tmux.conf https://gist.github.com/thestonefox/8883581/raw/193ad0c295c3da3422572173c1e1f2395bb87640/thestonefox-solarized-tmux

#Setup SSH Access
ONBUILD RUN mkdir -p /root/.ssh
ONBUILD RUN chown -R root:root /root/.ssh
ONBUILD RUN chmod -R 600 /root/.ssh/
ONBUILD RUN mkdir -p /var/run/sshd

ONBUILD RUN echo "source /etc/environment" >> /etc/profile

ONBUILD RUN rm -f /root/.ssh/authorized_keys /home/*/.ssh/authorized_keys
ONBUILD ADD id_rsa.pub /root/.ssh/id_rsa.pub
ONBUILD RUN cat /root/.ssh/id_rsa.pub > /root/.ssh/authorized_keys

#Initialise instance
ONBUILD RUN printf "#!/bin/bash \
\n if [ \${SSH_PASSWORD:+x} ] \
\n  then \
\n  echo "root:\$SSH_PASSWORD" |chpasswd \
\n fi \
\n env | grep _ | awk '{\$1 = \"export \" \$1; print}' > /etc/environment \
\n /usr/sbin/sshd -D" > /usr/local/bin/run

ONBUILD RUN chmod +x /usr/local/bin/run

ONBUILD VOLUME ["/var/www"]
ONBUILD CMD ["/usr/local/bin/run"]
