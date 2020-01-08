FROM ubuntu:latest
# USER root

ENV DEBIAN_FRONTEND=noninteractive USER=root PORT=5901 DISPLAY=:0.0 AUTHORITY=/root/.Xauthority

RUN apt-get update -y
RUN apt-get upgrade -y
#RUN apt-get install -y --no-install-recommends --allow-unauthenticated ubuntu-desktop ubuntu-gnome-desktop kubuntu-desktop
RUN apt-get install -y --allow-unauthenticated ubuntu-desktop ubuntu-gnome-desktop kubuntu-desktop
RUN apt-get install -y vim wget net-tools
RUN apt-get install -y tightvncserver

WORKDIR /root/

RUN apt-get install -y xfonts-100dpi xfonts-75dpi xfonts-tipa xfonts-scalable xfonts-cyrillic rxvt
RUN urxvt --help 2>&1| sed -n '/:  /s/^ */! URxvt*/gp' >> ~/.Xresources


EXPOSE $PORT

CMD ["/bin/bash"]
