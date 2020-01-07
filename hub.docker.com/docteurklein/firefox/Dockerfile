FROM debian:squeeze
RUN echo     && apt-get update     && apt-get -y install         bzip2         curl         xulrunner-1.9.1         libdbus-glib-1-2     && apt-get clean     && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN echo     && curl https://ftp.mozilla.org/pub/mozilla.org/firefox/releases/34.0.5/linux-x86_64/fr/firefox-34.0.5.tar.bz2 > firefox.bz2     && tar jxf firefox.bz2     && rm firefox.bz2
VOLUME [/root/.Xauthority, /tmp/.X11-unix]
ENTRYPOINT firefox/firefox
