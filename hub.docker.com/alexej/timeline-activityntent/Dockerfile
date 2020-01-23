FROM debian:stretch-slim

LABEL authors https://www.oda-alexandre.com/

ENV USER teamspeak
ENV HOME /home/${USER}
ENV LOCALES fr_FR.UTF-8

RUN echo -e '\033[36;1m ******* INSTALL PACKAGES ******** \033[0m'; \
  apt-get update && apt-get install --no-install-recommends -y \
  sudo \
  ca-certificates \
  wget \
  gnupg \
  dirmngr \
  locales \
  alsa-utils \
  libasound2 \
  libasound2-plugins \
  pulseaudio \
  pulseaudio-utils \
  libcanberra-gtk-module \
  libcanberra-gtk3-module \
  libgl1-mesa-dri \
  libgl1-mesa-glx \
  mesa-utils \
  xdg-utils \
  libgtk2.0-0 \
  libgconf-2-4 \
  libxtst6 \
  libxss1 \
  libnss3 \
  xvfb

RUN echo -e '\033[36;1m ******* CHANGE LOCALES ******** \033[0m'; \
  locale-gen ${LOCALES}

RUN echo -e '\033[36;1m ******* ADD USER ******** \033[0m'; \
  useradd -d ${HOME} -m ${USER}; \
  passwd -d ${USER}; \
  adduser ${USER} sudo

RUN echo -e '\033[36;1m ******* SELECT USER ******** \033[0m'
USER ${USER}

RUN echo -e '\033[36;1m ******* SELECT WORKING SPACE ******** \033[0m'
WORKDIR ${HOME}

RUN echo -e '\033[36;1m ******* ADD APP ******** \033[0m'
COPY ./teamspeak.sh  ${HOME}/teamspeak.sh

RUN sudo chmod +x ${HOME}/teamspeak.sh

RUN echo -e '\033[36;1m ******* CONTAINER START COMMAND ******** \033[0m'
CMD ./teamspeak.sh \