FROM kalilinux/kali-linux-docker:latest

MAINTAINER sp3nx0r <sp3nx0r@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm-256color
ENV USER root

RUN rm -fR /var/lib/apt/
RUN apt-get clean
RUN apt-get update -y
RUN apt-get install -y software-properties-common && apt-get update -y
RUN apt-get install -y kali-linux-full --fix-missing
RUN apt-get install -y git colordiff colortail unzip vim tmux xterm zsh curl telnet strace ltrace tmate less build-essential wget python3-setuptools python3-pip tor proxychains zstd
RUN git clone https://github.com/danielmiessler/SecLists /usr/share/seclists
RUN apt-get autoremove -y && apt-get autoclean
RUN updatedb

# Unzip rockyou if installed
RUN if [ -e /usr/share/wordlists/rockyou.txt.gz ]; then cd /usr/share/wordlists && gunzip rockyou.txt.gz ; fi

# Kali stuff should end up in the menus. Unfortunately this takes some effort.
RUN apt-get -y install menu-xdg
RUN apt-get -y install --reinstall kali-menu
RUN update-menus

# ngrok
RUN curl https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip | gunzip - > /usr/bin/ngrok
RUN chmod +x /usr/bin/ngrok

# gobuster
RUN wget https://github.com/OJ/gobuster/releases/download/v2.0.1/gobuster-linux-amd64.7z && 7z e -o/usr/bin/ gobuster-linux-amd64.7z  \
 && chmod +x /usr/bin/gobuster && rm gobuster-linux-amd64.7z

# wpscan update
RUN wpscan --update

# peda install

RUN git clone https://github.com/longld/peda.git /root/peda

# virtualenv config
RUN pip install virtualenvwrapper
RUN echo 'export WORKON_HOME=$HOME/.virtualenvs' >> /etc/profile
RUN echo 'export PROJECT_HOME=$HOME/projects' >> /etc/profile && mkdir /root/projects
RUN echo 'export VIRTUALENVWRAPPER_SCRIPT=/usr/local/bin/virtualenvwrapper.sh' >> /etc/profile
RUN bash /usr/local/bin/virtualenvwrapper.sh
RUN echo 'source /usr/local/bin/virtualenvwrapper.sh' >> /etc/profile

# Tor refresh every 5 requests
RUN echo MaxCircuitDirtiness 10 >> /etc/tor/torrc
# Tor start at init
RUN update-rc.d tor enable
# Use random proxy chains
RUN sed -i 's/^strict_chain/#strict_chain/g;s/^#random_chain/random_chain/g' /etc/proxychains.conf

### Install VNC and service setup ala https://github.com/wardwouts/kali-xfce ###

# Install a vnc server & openbox
RUN apt-get install -y tigervnc-standalone-server openssh-server supervisor xfce4 xfce4-places-plugin xfce4-goodies extra-xdg-menus

# Install noVNC
RUN apt-get -y install net-tools python python-numpy
RUN cd /root && git clone https://github.com/kanaka/noVNC.git
RUN cd /root/noVNC/utils && git clone https://github.com/kanaka/websockify websockify
RUN ln -s /root/noVNC/vnc.html /root/noVNC/index.html

# Add startup script
ADD startup.sh /startup.sh
RUN chmod 0755 /startup.sh

ADD supervisord.conf /
ADD root /root/
#################################################################################

# TBD add quality of life dotfile updates
RUN echo "set completion-ignore-case on" >> /etc/inputrc

# Ports to be exposed
EXPOSE 53
EXPOSE 80
EXPOSE 443
EXPOSE 4444
EXPOSE 8000
EXPOSE 8080
EXPOSE 8443
EXPOSE 31337
# VNC ports
EXPOSE 5901 6080

# Welcome message
RUN echo "echo 'Kali full container!\n\n- If you need proxychains over Tor just activate tor service with:\n$ service tor start\n'" >> /etc/profile

WORKDIR /pentest

CMD ["/bin/bash", "--init-file", "/etc/profile"]

ENTRYPOINT ["/startup.sh"]
