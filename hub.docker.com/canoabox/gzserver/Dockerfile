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
    mc mysql-client mysql-workbench leafpad vim python-pip
RUN easy_install 'supervisor == 3.2.0' 'supervisor-stdout == 0.1.1'    
RUN dpkg --add-architecture i386
RUN apt-get update
RUN apt-get install -y --force-yes \
	libc6:i386 openjdk-6-jdk:i386 openjdk-6-jre:i386
RUN apt-get autoclean && apt-get autoremove && rm -rf /var/lib/apt/lists/*
RUN update-alternatives --remove-all java \
	&& update-alternatives --install /usr/bin/java java /usr/lib/jvm/java-6-openjdk-i386/jre/bin/java 1

# Instalacao do GZ Server
RUN mkdir -p /opt/gz
WORKDIR /opt/gz
#RT - dependencia todos os programas
RUN wget http://gznet.com.br/download/containner/rt_linux_folder.tar.gz \
	&& tar zxvf rt_linux_folder.tar.gz \
	&& rm -f rt_linux_folder.tar.gz 
#FlexPlug - servidor
RUN wget http://gznet.com.br/download/containner/flexplug_linux_folder.tar.gz \
	&& tar zxvf flexplug_linux_folder.tar.gz \
	&& rm -f flexplug_linux_folder.tar.gz \
	&& cp -Rf rt flexplug/
#FlexDoor - servidor2
RUN wget http://gznet.com.br/download/containner/flexdoor_linux_folder.tar.gz \
	&& tar zxvf flexdoor_linux_folder.tar.gz \
	&& rm -f flexdoor_linux_folder.tar.gz \
	&& cp -Rf rt flexdoor/
#FlexBridge - servidor3
RUN wget http://gznet.com.br/download/containner/flexbridge_linux_folder.tar.gz \
	&& tar zxvf flexbridge_linux_folder.tar.gz \
	&& rm -f flexbridge_linux_folder.tar.gz \
	&& cp -Rf rt flexbridge/
#FlexConcent - programa gestao pdv
RUN wget http://gznet.com.br/download/containner/flexconcent_linux_folder.tar.gz \
	&& tar zxvf flexconcent_linux_folder.tar.gz \
	&& rm -f flexconcent_linux_folder.tar.gz \
	&& cp -Rf rt flexconcent/
#MercoFlex - programa gesta pdv e erp
RUN wget http://gznet.com.br/download/containner/mercoflex_linux_folder.tar.gz \
	&& tar zxvf mercoflex_linux_folder.tar.gz \
	&& rm -f mercoflex_linux_folder.tar.gz \
	&& cp -Rf rt mercoflex/
#FlexPrint
RUN wget http://gznet.com.br/download/containner/flexprint_linux_folder.tar.gz \
	&& tar zxvf flexprint_linux_folder.tar.gz \
	&& rm -f flexprint_linux_folder.tar.gz \
	&& cp -Rf flexprint flexconcent/ \
	&& cp -Rf flexprint mercoflex/ \
	&& rm -rf flexprint
#FlexBalcao
RUN wget http://gznet.com.br/download/containner/flexbalcao_linux_folder.tar.gz \
	&& tar zxvf flexbalcao_linux_folder.tar.gz \
	&& rm -f flexbalcao_linux_folder.tar.gz \ 
	&& cp -Rf rt flexbalcao/
#FlexFatur
RUN wget http://gznet.com.br/download/containner/flexfatur_linux_folder.tar.gz \
	&& tar zxvf flexfatur_linux_folder.tar.gz \
	&& rm -f flexfatur_linux_folder.tar.gz \
	&& cp -Rf rt flexfatur/
#GZNFCe
RUN wget http://gznet.com.br/download/containner/gznfce_linux_folder.tar.gz \
	&& tar zxvf gznfce_linux_folder.tar.gz \
	&& rm -f gznfce_linux_folder.tar.gz \
	&& cp -Rf rt gznfce/
#GZRMS
RUN wget http://gznet.com.br/download/containner/gzrms_linux_folder.tar.gz \
	&& tar zxvf gzrms_linux_folder.tar.gz \
	&& rm -f gzrms_linux_folder.tar.gz \
	&& cp -Rf rt gzrms/

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

EXPOSE 5900 4005-4515
VOLUME ["/opt/cd2/set", "/opt/gz/flexplug/properties", "/opt/gz/flexdoor/properties", "/opt/gz/flexbridge/properties", "/opt/gz/flexconcent/properties", "/opt/gz/mercoflex/properties"]
CMD ["/usr/local/bin/supervisord", "--configuration=/etc/supervisor/supervisord.conf"]