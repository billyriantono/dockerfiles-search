FROM cmptech/guidocker
MAINTAINER FanLin <linfan.china@gmail.com>
MAINTAINER wanjo <https://github.com/wanjochan/

RUN apt-get update -y

# VNC, Xvfb, Fluxbox
RUN apt-get -qqy --force-yes install x11vnc xvfb fluxbox rxvt-unicode

# build passwd for x11vnc as "vncpass".... please change it when go online...
RUN mkdir -p ~/.vnc && x11vnc -storepasswd vncpass ~/.vnc/passwd

# cleanup
RUN apt-get autoclean && apt-get autoremove && rm -rf /var/lib/apt/lists/*

# https://journal.paul.querna.org/articles/2013/10/15/docker-ubuntu-on-rackspace/
# To allow automated installation of new packages, set the debconf(7) frontend to noninteractive, which never prompts the user for choices on installation/configuration of packages:
ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true

# screen default
ENV SCREEN_WIDTH 1360
ENV SCREEN_HEIGHT 1020
ENV SCREEN_DEPTH 24

ENV DISPLAY :99.0

EXPOSE 5900

#RUN echo "Section \"InputDevice\"\n\
#Identifier  \"Mouse0\"\n\
#Driver      \"mouse\"\n\
#Option      \"Device" "/dev/mouse\"\n\
#Option      \"Protocol\" \"PS/2\"\n\
#Option      \"Emulate3Buttons\" \"on\"\n\
#EndSection" >> /etc/X11/xorg.conf

COPY entry_point.sh /opt/bin/entry_point.sh
RUN chmod +x /opt/bin/entry_point.sh

CMD ["/opt/bin/entry_point.sh"]

