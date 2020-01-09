# Parent image
FROM barexte/wimo

MAINTAINER BAREXTE <barexte@gmail.com>

# Install lib32gcc1, wine and create steam user
RUN \
  dpkg --add-architecture i386 && \
  apt update && \
  apt upgrade -y && \
  apt install lib32gcc1 curl -y && \
  apt install --install-recommends winehq-stable xvfb -y && \
  useradd -m steam 

# Configure environment
USER steam
WORKDIR /home/steam
ENV HOME=/home/steam WINEDEBUG=-all

# Install dependency in wine
RUN \
  wget 'https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks' && \
  chmod +x ~/winetricks && \
  ~/winetricks winxp && \
  wget 'http://download.microsoft.com/download/9/5/A/95A9616B-7A37-4AF6-BC36-D6EA96C8DAAE/dotNetFx40_Full_x86_x64.exe' && \
  wine ~/dotNetFx40_Full_x86_x64.exe /q && \
  ~/winetricks win7 && \
  wget 'https://download.visualstudio.microsoft.com/download/pr/7afca223-55d2-470a-8edc-6a1739ae3252/abd170b4b0ec15ad0222a809b761a036/ndp48-x86-x64-allos-enu.exe' && \
  wine ~/ndp48-x86-x64-allos-enu.exe /q && \
  xvfb-run -a ~/winetricks -q vcrun2013 && \
  xvfb-run -a ~/winetricks -q vcrun2017
 
# Install SteamCMD
RUN \
  mkdir ~/se-server && \
  mkdir ~/Steam && \
  cd ~/Steam && \
  curl -sqL "https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz" | tar zxvf -
 
# Install SE Server
RUN \
  cd ~/Steam && \
  ./steamcmd.sh +login anonymous +force_install_dir "/home/steam/se-server/" +app_update 298740 +quit

# switch user
USER root
