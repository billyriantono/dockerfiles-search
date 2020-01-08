FROM bwbush/vnc

MAINTAINER Brian W Bush <root@bwbush.io>

USER root

RUN wget -q -O - http://dl-ssl.google.com/linux/linux_signing_key.pub \
 |  apt-key add -                                                     \
 && echo "deb http://dl.google.com/linux/chrome/deb/ stable main"     \
      > /etc/apt/sources.list.d/google.list                           \
 && apt-get update                                                    \
 && apt-get install --no-install-recommends --yes                     \
      google-chrome-stable                                            \
      lxde                                                            \
      x11vnc                                                          \
#     xfce4                                                           \
      xfonts-base                                                     \
      xvfb                                                            \
 && apt-get clean autoclean                                           \
 && apt-get autoremove --yes

USER vnc-user

RUN echo '#!/bin/bash'                                                                               \
      >  .xinitrc                                                                                    \
 && echo 'exec /opt/google/chrome/chrome --no-sandbox --window-position=0,0 --window-size=1250,1000' \
      >> .xinitrc                                                                                    \
 && chmod +x .xinitrc
