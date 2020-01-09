FROM ubuntu:trusty

MAINTAINER Alan Quach <integsrtite@gmail.com>

ENV TZ=America/Los_Angeles
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN locale-gen en_US.UTF-8

RUN apt-get update && apt-get install -y openssh-server
RUN mkdir /var/run/sshd

# CORE
RUN apt-get update && apt-get install -y ca-certificates
RUN apt-get update && apt-get install -y curl
RUN apt-get update && apt-get install -y zip unzip tar
RUN apt-get update && apt-get install -y dnsutils
RUN apt-get update && apt-get install -y man
RUN apt-get update && apt-get install -y build-essential
RUN apt-get update && apt-get install -y cmake python-dev python3-dev
RUN apt-get update && apt-get install -y tmux
RUN apt-get update && apt-get install -y git
RUN apt-get update && apt-get install -y vim
RUN apt-get update && apt-get install -y mosh
RUN apt-get update && apt-get install -y python3-pip

# UI
RUN apt-get update && apt-get install -y tightvncserver
# RUN curl -Lv https://dl.bintray.com/tigervnc/stable/tigervnc-1.7.0.x86_64.tar.gz -o /tmp/tigervnc-1.7.0.x86_64.tar.gz
# RUN tar -xvf /tmp/tigervnc-1.7.0.x86_64.tar.gz -C /tmp
# RUN rsync -avz /tmp/tigervnc*/usr/ /usr
# RUN apt-get update && apt-get install -y x11-xkb-utils
RUN apt-get update && apt-get install -y i3
RUN apt-get update && apt-get install -y terminator
# RUN setcap -r `which i3status`

# RUN apt-get update && apt-get install -y dmenu
# RUN apt-get update && apt-get install -y dunst
# RUN apt-get update && apt-get install -y connman-ui
# RUN apt-get update && apt-get install -y feh
# RUN apt-get update && apt-get install -y rox-filer

# No need to embed authorized_keys at build time, simply exec echo them into the container at runtime:
# docker exec primedev /bin/sh -c "echo \"$(cat dotssh/authorized_keys)\" > /root/.ssh/authorized_keys"

# # RUN git clone https://github.com/spf13/spf13-vim.git /root/git/spf13-vim
# # RUN cd /root/git/spf13-vim && git checkout "3.0" && /root/git/spf13-vim/bootstrap.sh
# # RUN vim +BundleInstall +qall
# # RUN NVM_DIR=/root/.nvm && . /root/.nvm/nvm.sh && /root/.vim/bundle/YouCompleteMe/install.py --tern-completer

RUN apt-get install -y software-properties-common
# RUN add-apt-repository -y ppa:openjdk-r/ppa
# RUN apt-get update && apt-get install -y openjdk-8-jdk
RUN apt-add-repository -y ppa:webupd8team/java
RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections
RUN apt-get update && apt-get install -y oracle-java8-installer
RUN wget https://download.jetbrains.com/idea/ideaIC-2016.2.5.tar.gz -O /tmp/intellij.tar.gz -q && \
    echo 'Installing IntelliJ IDEA' && \
    mkdir -p /opt/intellij && \
    tar -xf /tmp/intellij.tar.gz --strip-components=1 -C /opt/intellij && \
    rm /tmp/intellij.tar.gz && \
    echo -ne '#!/bin/bash'"\n\nexec /opt/intellij/bin/idea.sh\n" > /usr/local/bin/intellij && \
    chmod a+x /usr/local/bin/intellij

ENV user aquach
RUN adduser --gecos "" $user && adduser $user sudo && echo "$user:$user" | chpasswd && passwd -e aquach
USER $user
RUN mkdir /home/$user/.ssh
RUN mkdir /home/$user/.vnc
RUN echo 'localhost' > /home/$user/.vnc/config
# ADD xstartup /home/$user/.vnc/xstartup
# the below echo is a hack until the ADD directive gets proper permission setting options (https://github.com/docker/docker/pull/27303)
RUN echo $'#!/bin/sh\n\n[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup\n[ -r \$HOME/.Xresources ] && xrdb \$HOME/.Xresurces\nexec i3 &\n' > /home/$user/.vnc/xstartup
RUN chmod +x /home/$user/.vnc/xstartup
RUN mkdir /home/$user/.i3
RUN cp /etc/i3/config /home/$user/.i3/config
RUN echo "exec i3" > /home/$user/.xinitrc

RUN git clone https://github.com/alanmquach/dotfiles.git /home/$user/dotfiles
RUN /home/$user/dotfiles/bootstrap.sh -f
RUN pip3 install --user pygments

RUN git clone https://github.com/creationix/nvm.git /home/$user/.nvm
RUN NVM_DIR=/home/$user/.nvm && . /home/$user/.nvm/nvm.sh && nvm install stable

# vncpasswd; echo -ne '#!/bin/sh'"\n\n[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup\n[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresurces\nexec i3 &\n" > ~/.vnc/xstartup; chmod +x ~/.vnc/xstartup; echo "exec i3" > ~/.xinitrc; mkdir ~/.i3; cp /etc/i3/config ~/.i3/config
# vncserver :2 -geometry 1680x1050 -depth 24
# JAVA_HOME="/usr/lib/jvm/java-8-oracle/jre/bin/java"

EXPOSE 22
EXPOSE 60000-60010

USER root

CMD ["/usr/sbin/sshd", "-D"]

