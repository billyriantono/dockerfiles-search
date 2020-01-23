FROM ubuntu:14.04
MAINTAINER CD2 Tecnologia <suporte@cd2.com.br>
ENV DEBIAN_FRONTEND noninteractive
ENV HOME /root
ENV VNC_PASSWORD 81215111
ENV DISPLAY :10.0
#Instalar dependencias
RUN apt-get update 
RUN apt-get install -y --force-yes --no-install-recommends \
    xinetd x11vnc xvfb tinywm openbox xdotool wmctrl x11-utils \
    xterm wget openbox obconf menu obmenu software-properties-common \
    python-software-properties dbus hicolor-icon-theme pcmanfm lxpanel \
    mc leafpad vim python-pip
RUN easy_install 'supervisor == 3.2.0' 'supervisor-stdout == 0.1.1'    
#Config minimal desktop
RUN mkdir -p /root/Desktop/
ADD ./desktop/Desktop /root/Desktop
RUN mkdir -p /root/.config/lxpanel/default/panels/
ADD ./desktop/panel /root/.config/lxpanel/default/panels/panel
RUN mkdir -p /root/.config/pcmanfm/default
ADD ./desktop/desktop-items-0.conf /root/.config/pcmanfm/default/desktop-items-0.conf
ADD ./desktop/pcmanfm.conf /root/.config/pcmanfm/default/pcmanfm.conf

#Config supervisord
RUN mkdir -p /var/log/supervisor
ADD ./supervisor/supervisord.conf /etc/supervisor/supervisord.conf
ADD ./supervisor/conf.d /etc/supervisor/conf.d

#Install first start
RUN mkdir -p /opt/cd2/defaults
WORKDIR /opt/cd2
ADD ./cd2/defaults /opt/cd2/defaults 
ADD ./cd2/firstboot.sh /opt/cd2/firstboot.sh
RUN touch /opt/cd2/firstboot.run

EXPOSE 5900 
VOLUME ["/opt/cd2/set"]
CMD ["/usr/local/bin/supervisord", "--configuration=/etc/supervisor/supervisord.conf"]
