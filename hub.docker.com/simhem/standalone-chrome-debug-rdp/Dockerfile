FROM selenium/standalone-chrome-debug:3.4.0-francium

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

#===============
# XRDP settings
#===============
 RUN apt-get update -y \
  && apt-get -y install \
  xrdp \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/*

# ADD xrdp.deb /tmp/ 
# RUN dpkg -i /tmp/xrdp.deb
# RUN rm -rf /tmp/xrdp.deb

# ADD language-pack-fr-base.deb /tmp/
# ADD language-pack-fr.deb /tmp/
# RUN dpkg -i /tmp/language-pack-fr.deb /tmp/language-pack-fr-base.deb
# RUN rm -rf /tmp/language-pack-fr-base.deb
# RUN rm -rf /tmp/language-pack-fr.deb

USER seluser

ADD xrdp.ini /etc/xrdp/

# RUN sed -i 's/^Terminal/#&/' /etc/xrdp/sesman.ini
RUN sudo sed -i '/x11vnc /a sudo \/etc\/init.d\/xrdp start &' /opt/bin/entry_point.sh

EXPOSE 3389

