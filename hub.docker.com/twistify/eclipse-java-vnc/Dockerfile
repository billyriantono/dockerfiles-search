# BUILD: sudo docker build -t eclipse-java-vnc .
# TEST RUN: sudo docker run -it --rm -d -p5901:5901 --name eclipse eclipse-java-vnc

FROM ubuntu:16.04

LABEL maintainer "@twistify"
LABEL description "Eclipse Neon on Ubuntu over VNC"


# install base packages required
RUN   apt-get update \
  &&  apt-get install -y --no-install-recommends xfce4 \
        xfce4-goodies \
        xfce4-artwork \
        xfonts-base \
        xfonts-encodings \
        gnome-icon-theme-full \
        tango-icon-theme \
        sudo \
        software-properties-common \
        tightvncserver


# install oracle java 8 JDK and silently accept license
RUN     apt-get update \
    &&  apt-get install -y software-properties-common \
    &&  add-apt-repository ppa:webupd8team/java \
    &&  apt-get update \
    &&  echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections \
    &&  echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 seen true" | debconf-set-selections \
    &&  apt-get install -y oracle-java8-installer \
    &&  apt install oracle-java8-set-default \
    &&  rm -rf /var/lib/apt/lists/*

# install eclipse (use --no-install-recommends to avoid installing OpenJDK)
COPY eclipse.desktop /usr/share/applications/eclipse.desktop

RUN     cd /tmp \
    &&  wget http://download.eclipse.org/technology/epp/downloads/release/neon/2/eclipse-java-neon-2-linux-gtk-x86_64.tar.gz

RUN     cd /tmp \
    &&  tar xvf eclipse-java-neon-2-linux-gtk-x86_64.tar.gz \
    &&  mv eclipse /opt \
    &&  rm -R eclipse* \
    &&  desktop-file-install /usr/share/applications/eclipse.desktop \
    &&  cd /usr/local/bin \
    &&  ln -s /opt/eclipse/eclipse

# set some labels so users can easily find the VNC access details
ENV VNC_PASSWORD=eclipse
ENV VNC_RESOLUTION=1024x768
ENV USERNAME=eclipse
ENV PASSWORD=eclipse

# copy and prepare our startup script
COPY startup.sh /startup.sh
RUN     chmod +x /startup.sh

# expose our VNC port
EXPOSE 5901

# set our volume
VOLUME /home

# start our vncserver
ENTRYPOINT ["./startup.sh"]
