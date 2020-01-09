FROM ubuntu:bionic

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update; apt-get clean

# Add a user for running applications.
RUN useradd apps
RUN mkdir -p /home/apps && chown apps:apps /home/apps

# Install x11vnc.
RUN apt-get install -y x11vnc xvfb nano pulseaudio mpv wget python screen fluxbox wmctrl xdotool software-properties-common

# Set the Chrome repo.
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list

# Install Chrome and ffmpeg.
RUN apt-get update && apt-get -y install google-chrome-stable ffmpeg

COPY bootstrap.sh /

CMD '/bootstrap.sh'