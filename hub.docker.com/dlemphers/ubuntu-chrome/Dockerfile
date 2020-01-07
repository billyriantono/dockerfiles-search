FROM ubuntu:16.04

LABEL maintainer="dlemphers@gmail.com"

RUN apt-get update && apt-get install wget -y

RUN wget -q -O - "https://dl-ssl.google.com/linux/linux_signing_key.pub" | apt-key add - \
 && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list

RUN apt-get update -y

COPY local.conf /etc/fonts/local.conf

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y xz-utils file locales dbus-x11 pulseaudio dmz-cursor-theme curl \
      fonts-dejavu fonts-liberation hicolor-icon-theme \
      libcanberra-gtk3-0 libcanberra-gtk-module libcanberra-gtk3-module \
      libasound2 libglib2.0 libgtk2.0-0 libdbus-glib-1-2 libxt6 libexif12 \
      libgl1-mesa-glx libgl1-mesa-dri libstdc++6 nvidia-346 \
      gstreamer-1.0 gstreamer1.0-plugins-base gstreamer1.0-plugins-good \
      gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav \
      google-chrome-stable