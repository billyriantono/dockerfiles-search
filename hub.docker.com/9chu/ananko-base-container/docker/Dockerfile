FROM ubuntu:18.04
MAINTAINER Sad Cactus
ENV DEBIAN_FRONTEND noninteractive
RUN mkdir -p ~/desktop
RUN apt-get -y update
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:jonathonf/mate-1.20
RUN apt-get -y update
RUN apt install -y libcurl4 vim wget ca-certificates xorgxrdp pulseaudio xrdp\
   	xauth supervisor uuid-runtime locales \
   	pepperflashplugin-nonfree openssh-server sudo \
  	nano curl git unzip  python-pip firefox xvfb  python3-pip gedit locate tor libxml2-dev libxslt1-dev mysql-server libmysqlclient-dev byobu locate mate-core ubuntu-mate-themes  \
    mate-desktop-environment mate-notification-daemon \
    gconf-service libnspr4 libnss3 fonts-liberation \
    libappindicator1  fonts-wqy-microhei  && \
    apt-get autoclean && apt-get autoremove && \
    rm -rf /var/lib/apt/lists/* && \
    echo "mate-session" > ~/.xsession

RUN XDG_DATA_DIRS=/usr/share/mate:/usr/share/mate:/usr/local/share
RUN XDG_DATA_DIRS=${XDG_DATA_DIRS}:/usr/share:/var/lib/snapd/desktop
ADD bin /usr/bin
ADD etc /etc
ADD otob /root
RUN ls
RUN mkdir -p ~/.mozilla/firefox
RUN mkdir -p ~/.ssh
RUN rm /etc/ssh/sshd_config
RUN locale-gen en_US.UTF-8
RUN cp /root/sshd_config /etc/ssh/
RUN cp /root/authorized_keys  ~/.ssh/authorized_keys
RUN cp /root/xsessionrc  ~/.xsessionrc

RUN rm -rf /etc/xrdp/rsakeys.ini /etc/xrdp/*.pem
RUN sed -e 's/^new_cursors=true/new_cursors=false/g' -i /etc/xrdp/xrdp.ini
RUN echo "export PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '" >> ~/.bashrc
RUN echo "export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games" >> ~/.bashrc
RUN echo "export LC_ALL='en_US.utf8'" >> ~/.bashrc

RUN wget https://github.com/mozilla/geckodriver/releases/download/v0.23.0/geckodriver-v0.23.0-linux64.tar.gz 
RUN tar -xvf geckodriver-v0.23.0-linux64.tar.gz
RUN chmod +x geckodriver
RUN cp geckodriver /usr/bin/geckodriver

RUN pip3 install pyvirtualdisplay faker-e164 Faker mysql-connector PySocks stem torrequest bs4 selenium mysqlclient ConfigParser pymysql lxml fake_useragent




# Add sample user fg gor
RUN update-rc.d tor enable
RUN ssh-keygen -q -t rsa -N '' -f /id_rsa
RUN echo "root:1" | /usr/sbin/chpasswd
RUN addgroup uno
RUN useradd -m -s /bin/bash -g uno uno
RUN echo "uno:1" | /usr/sbin/chpasswd
RUN echo "uno    ALL=(ALL) ALL" >> /etc/sudoers


# Docker config

RUN tar -xvf /root/hbxtyfcz.00a001.tar.gz -C /root/.mozilla/firefox
RUN tar -xvf /root/prof0_0.tar.gz -C /root/Qookie