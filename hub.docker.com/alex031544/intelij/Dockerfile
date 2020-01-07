FROM openjdk:13-alpine

RUN apk add xorg-server xf86-video-vesa xf86-input-evdev xf86-input-mouse xf86-input-keyboard udev git wget maven ttf-dejavu

ENV intelijVersion=ideaIC-2019.1.3
ENV intelijPath=idea-IC-191.7479.19

RUN wget https://download.jetbrains.com/idea/${intelijVersion}.tar.gz
RUN mkdir /opt/intelij
RUN tar -xf ${intelijVersion}.tar.gz -C /opt/intelij
RUN rm ${intelijVersion}.tar.gz
ADD idea64.vmoptions /opt/intelij/${intelijPath}/bin/idea64.vmoptions
ADD idea.properties /opt/intelij/${intelijPath}/bin/idea.properties

VOLUME /data

CMD /opt/intelij/${intelijPath}/bin/idea.sh
