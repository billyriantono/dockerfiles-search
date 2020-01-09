FROM debian:stretch-slim

LABEL authors https://www.oda-alexandre.com/

ENV USER teamspeak
ENV HOME /home/${USER}
ENV LOCALES fr_FR.UTF-8
ENV VERSION 3.6.1
ENV DEBIAN_FRONTEND noninteractive

RUN echo -e '\033[36;1m ******* INSTALL PACKAGES ******** \033[0m'; \
  apt-get update && apt-get install --no-install-recommends -y \
  sudo \
  locales \
  apt-transport-https \
  ca-certificates \
  bzip2 \
  wget

RUN echo -e '\033[36;1m ******* CHANGE LOCALES ******** \033[0m'; \
  locale-gen ${LOCALES}

RUN echo -e '\033[36;1m ******* ADD USER ******** \033[0m'; \
  useradd -d ${HOME} -m ${USER}; \
  passwd -d ${USER}; \
  adduser ${USER} sudo

RUN echo -e '\033[36;1m ******* SELECT USER ******** \033[0m'
USER ${USER}

RUN echo -e '\033[36;1m ******* CREATE END SECURE WORKING SPACE ******** \033[0m'; \
  sudo mkdir /opt/teamspeak; \
  sudo chown -R ${USER}:${USER} /opt/teamspeak; \
  sudo chmod 0770 /opt/teamspeak

RUN echo -e '\033[36;1m ******* SELECT WORKING SPACE ******** \033[0m'
WORKDIR /opt/teamspeak

RUN echo -e '\033[36;1m ******* INSTALL APP ******** \033[0m'; \
  wget https://files.teamspeak-services.com/releases/server/${VERSION}/teamspeak3-server_linux_amd64-${VERSION}.tar.bz2; \
  tar xvf teamspeak3-server_linux_amd64-${VERSION}.tar.bz2; \
  echo "license_accepted=1" >> teamspeak3-server_linux_amd64/.ts3server_license_accepted; \
  rm -rf teamspeak3-server_linux_amd64-${VERSION}.tar.bz2

RUN echo -e '\033[36;1m ******* CLEANING ******** \033[0m'; \
  sudo apt-get --purge autoremove -y \
  bzip2 \
  wget; \
  sudo apt-get autoclean -y; \
  sudo rm /etc/apt/sources.list; \
  sudo rm -rf /var/cache/apt/archives/*; \
  sudo rm -rf /var/lib/apt/lists/*

RUN echo -e '\033[36;1m ******* SELECT WORKING SPACE ******** \033[0m'
WORKDIR /opt/teamspeak/teamspeak3-server_linux_amd64

RUN echo -e '\033[36;1m ******* CONTAINER START COMMAND ******** \033[0m'
CMD ./ts3server_minimal_runscript.sh \