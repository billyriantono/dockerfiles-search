FROM buildpack-deps:eoan

### base.Dockerfile
### Generator: https://github.com/zerdos/devcontainer/
LABEL maintainer=zoltan.erdos@me.com

ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Europe/London

RUN apt-get update \
  && apt-get install --no-install-recommends -y \
    software-properties-common \
    apt-utils \
    ssh-client \
    make \
    gcc \
    gpg \
    htop \
    dos2unix \
    g++ \
    libvips \
    python2.7 \
    xz-utils \
    libx11-dev \
    dirmngr \
    curl \
    xz-utils \
    apt-transport-https \
    nano \
    mc \
    zsh \
    tzdata \
    sudo \
    locales \
    && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8 \
    && addgroup --gid 1024 devgroup \
    && adduser --uid 1024 --disabled-password --gecos "" --force-badname --shell /usr/bin/zsh --ingroup devgroup developer \
    && adduser developer sudo \
    && chown developer:devgroup -R /home/developer \
    && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers \
    && touch /usr/bin/startx /usr/bin/startWithBash \
    && chmod +x /usr/bin/startx /usr/bin/startWithBash \
    && echo "sudo sysctl fs.inotify.max_user_watches=524288 fs.inotify.max_user_instances=524288 net.core.somaxconn=524288 scache.object_max_active=524288 && sudo sysctl -p" >> /usr/bin/startx \
    && echo "bash /usr/bin/startx">> /usr/bin/startWithBash && chmod +x /usr/bin/startWithBash \
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/lib/apt/lists/* 

ENV LANG en_US.utf8

### noVNC.Dockerfile

RUN  apt-get update \
  && apt-get install --no-install-recommends -y \
    autocutsel \
    xfwm4 \
    libgtk-3-0 \
    xvfb \
    novnc \
    websockify \
    dbus-x11 \
    nano \
    mc \
    htop \
    procps \  
    terminator \
    tigervnc-standalone-server tigervnc-xorg-extension \
  &&  cp /usr/share/novnc/vnc.html /usr/share/novnc/index.html \
  && sed -i -e '1 aautocutsel -fork' /etc/X11/Xvnc-session \
  && sed -i -e 's/iconic/nowin/g' /etc/X11/Xvnc-session \
  && sed -i -e 's/workspace_count=4/workspace_count=1/g' /usr/share/xfwm4/defaults \
  && sed -i -e 's/use_compositing=true/use_compositing=false/g' /usr/share/xfwm4/defaults \
  && sed -i -e '1 aterminator &' /etc/X11/Xvnc-session \
  && apt-get autoremove -y \
  && apt-get clean -y \
  && rm -rf /var/lib/apt/lists/* \
  && echo "(chmod 644 ~/.ssh/*.pub && chmod 600 ~/.ssh/id_rsa && chmod 600 ~/.gitconfig || true ) && (vncserver -SecurityTypes none -cleanstale -useold :1 -localhost no --I-KNOW-THIS-IS-INSECURE && websockify --web=/usr/share/novnc/ --wrap-mode=ignore 6080 localhost:5901 || echo ok)" >> /usr/bin/startx

### xfce.Dockerfile

RUN apt-get update \
    && apt-get install --no-install-recommends -y \
        xfce4 \
        xfce4-goodies  \
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* 

    
### chromium.Dockerfile
RUN  curl -sSL  https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list \
    && apt-get update && apt-get install  -y google-chrome-stable \
     && apt-get autoremove -y \
  && apt-get clean -y \
  && rm -rf /var/lib/apt/lists/*

### zsh.Dockerfie

USER developer
ENV HOME /home/developer
WORKDIR /home/developer
ENV SHELL=/usr/bin/zsh
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" \
    && sed -i -e 's/plugins=(git)/plugins=(git gitfast git-extras npm yarn)/g' .zshrc 

CMD startWithBash
### suffix.Dockerfie


CMD bash startx