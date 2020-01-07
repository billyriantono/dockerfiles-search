FROM ubuntu:14.04

RUN echo "deb http://archive.ubuntu.com/ubuntu/ trusty main universe multiverse restricted" > /etc/apt/sources.list
RUN echo "deb http://archive.ubuntu.com/ubuntu/ trusty-updates main universe multiverse restricted" >> /etc/apt/sources.list
run apt-get update
run echo ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula \
    select true | debconf-set-selections
run apt-get install --no-install-recommends --yes --force-yes xorg xvfb x11-xkb-utils xfonts-100dpi xfonts-75dpi xfonts-scalable xfonts-cyrillic x11-apps cabextract xfonts-intl-chinese xfonts-intl-chinese-big cabextract ttf-mscorefonts-installer wget libgtk2.0-0 libgconf-2-4 libasound2 libxtst6 libxss1 libnss3 libnotify4 libexif-dev build-essential sendmail
run mkfontdir
run apt-get install -y curl
run curl -sL https://deb.nodesource.com/setup_5.x | sudo -E bash -
run apt-get install -y nodejs
