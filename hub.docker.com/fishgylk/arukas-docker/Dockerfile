FROM       ubuntu:17.04
MAINTAINER Aleksandar Diklic "https://github.com/rastasheep"

RUN apt-get update

RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd

RUN echo 'root:root123' |chpasswd

RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/g' /etc/ssh/sshd_config
RUN sed -ri 's/prohibit-password/yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

EXPOSE 22

# My custom
WORKDIR /root/

#RUN echo 'deb http://archive.ubuntu.com/ubuntu/ xenial-security multiverse' >> /etc/apt/sources.list
#RUN echo 'deb-src http://archive.ubuntu.com/ubuntu/ xenial-security multiverse' >> /etc/apt/sources.list

RUN apt-get update && apt-get install m2crypto git vim  mtr vnstat  curl wget cron screen -y 


#RUN wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.9.9/linux-headers-4.9.9-040909_4.9.9-040909.201702090333_all.deb
#RUN wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.9.9/linux-headers-4.9.9-040909-generic_4.9.9-040909.201702090333_amd64.deb
#RUN wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v4.9.9/linux-image-4.9.9-040909-generic_4.9.9-040909.201702090333_amd64.deb
#RUN dpkg -i *.deb
#RUN update-grub

# download extra
# RUN wget https://addons.mozilla.org/firefox/downloads/latest/vagex-firefox-add-on/addon-321174-latest.xpi \
#&& wget https://www.ebesucher.com/data/firefoxaddon/latest.xpi

#RUN git clone -b manyuser https://github.com/shadowsocksr/shadowsocksr.git	

# xvnc server porst, if $DISPLAY=:1 port will be 5901	
EXPOSE 15900	
# tinyproxy server porst
EXPOSE 8888		
# shadowsocksr server porst
EXPOSE 1080


ADD scripts /root

RUN chmod a+x /root/*.sh  
RUN echo '*/1 * * * * root bash /root/check.sh' >> /etc/crontab
RUN service cron restart
#RUN service tinyproxy restart


CMD    ["/usr/sbin/sshd", "-D"]
