FROM fedora:21
MAINTAINER elisadpc mainetti@apc.in2p3.fr
#Based upon fedora/firefox
#
# Install the appropriate software
RUN yum -y update && yum clean all
RUN yum -y install xorg-x11-twm tigervnc-server \
xterm xorg-x11-font \
xulrunner-26.0-2.fc20.x86_64 \
dejavu-sans-fonts \
dejavu-serif-fonts \
xdotool git tar wget && yum clean all

RUN yum -y install numpy scipy python-matplotlib

# Add the xstartup file into the image and set the default password.
RUN mkdir /root/.vnc
ADD ./xstartup /root/.vnc/
RUN chmod -v +x /root/.vnc/xstartup
RUN echo 123456 | vncpasswd -f > /root/.vnc/passwd
RUN chmod -v 600 /root/.vnc/passwd

RUN sed -i '/\/etc\/X11\/xinit\/xinitrc-common/a [ -x /usr/bin/firefox ] && /usr/bin/xterm &' /etc/X11/xinit/xinitrc

EXPOSE 5901

RUN mkdir /workspace && cd /workspace &&  git clone https://gitlab.in2p3.fr/elisadpc/eLISAToolBox.git && wget http://www.apc.univ-paris7.fr/Downloads/lisa/eLISA/Sensitivity/Cfgv1/StochBkgd/StochBkgdSNR_Cfgv1.0_v0.3.tar.gz && tar -zxvf StochBkgdSNR_Cfgv1.0_v0.3.tar.gz && wget http://www.apc.univ-paris7.fr/Downloads/lisa/eLISA/Sensitivity/Cfgv1/StochBkgd/StochBkgdSNR_Cfgv1.1.tar.gz && tar -zxvf StochBkgdSNR_Cfgv1.1.tar.gz && rm *.tar.gz

CMD    ["vncserver", "-fg" ]

