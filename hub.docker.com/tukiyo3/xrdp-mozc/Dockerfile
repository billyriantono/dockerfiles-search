FROM ubuntu:xenial
ENV DEBIAN_FRONTEND noninteractive

## add packages
RUN echo 'apt-get update -qq && apt-get install -yq $@ && apt-get clean && rm -rf /var/lib/apt/lists/*' > /usr/local/bin/apt.sh \
    && chmod +x /usr/local/bin/apt.sh \
    && sed -i -e 's/archive/jp.archive/g' /etc/apt/sources.list

## set timezone
RUN apt.sh tzdata
RUN ln -s -f /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
    && dpkg-reconfigure tzdata

RUN apt.sh ibus-mozc locales
RUN sed -i -e "s/^enabled=True/enabled=False/" /etc/xdg/user-dirs.conf \
    && sed -i -e "s/^# ja_JP.UTF-8/ja_JP.UTF-8/" /etc/locale.gen \
    && locale-gen \
    && update-locale LANG="ja_JP.UTF-8"
## ibus
ENV LANG "ja_JP.UTF-8"

RUN apt.sh \
      fonts-takao xrdp lxde-core 

RUN apt.sh \
      sudo vim-gtk wget tightvncserver \
      fizsh ssh autossh expect rdesktop xtightvncviewer \
      xfce4-terminal xfce4-screenshooter firefox thunderbird \
      git tig ranger mutt w3m nkf
      
WORKDIR /etc/xrdp
COPY files/xrdp/km-e0010411.ini km-0411.ini
RUN chmod 644 km-0411.ini \
    && ln -s km-0411.ini km-e0010411.ini \
    && ln -s km-0411.ini km-e0200411.ini \
    && ln -s km-0411.ini km-e0210411.ini

## create vagrant account.uid:gid=1000:1000
ENV USER vagrant
ENV PASSWORD ci9Ab0ro
ENV HOME /home/${USER}
RUN export uid=1000 gid=1000 \
    && echo "${USER}:x:${uid}:${gid}:Developer,,,:${HOME}:/usr/bin/fizsh" >> /etc/passwd \
    && echo "${USER}:x:${uid}:" >> /etc/group \
    && echo "${USER} ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers \
    && echo "${USER}:${PASSWORD}" | chpasswd \
    && mkdir -p .config/lxsession/LXDE/ \
    && echo "@ibus-daemon -d" >> .config/lxsession/LXDE/autostart
WORKDIR ${HOME}

RUN chown -R "${USER}:${USER}" ${HOME}

#VOLUME ${HOME}
EXPOSE 3389
CMD (rm -f /var/run/xrdp/*; /etc/init.d/xrdp start; tail -f /dev/null)
