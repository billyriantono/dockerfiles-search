FROM selenium/node-chrome-debug:3.7.0-arsenic

USER root

#===================
# Timezone settings
# Possible alternative: https://github.com/docker/docker/issues/3359#issuecomment-32150214
#===================
ENV TZ "Europe/Paris"
RUN echo "${TZ}" > /etc/timezone \
  && dpkg-reconfigure --frontend noninteractive tzdata

#=================
# Locale settings
#=================

ENV LANGUAGE fr_FR.UTF-8
ENV LANG fr_FR.UTF-8
RUN locale-gen fr_FR.UTF-8 \
  && dpkg-reconfigure --frontend noninteractive locales \
  && apt-get update -y \
  && apt-get -y --no-install-recommends install \
  language-pack-fr \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/*

RUN mkdir -p ~/.vnc \
  && x11vnc -storepasswd secret ~/.vnc/passwd

USER seluser

RUN sudo sed -i '4i echo $SCREEN_WIDTH"x"$SCREEN_HEIGHT' /opt/bin/entry_point.sh
RUN sudo sed -i '/x11vnc /c x11vnc -forever -shared -rfbport 5900 -display $DISPLAY &' /opt/bin/entry_point.sh

EXPOSE 3389
