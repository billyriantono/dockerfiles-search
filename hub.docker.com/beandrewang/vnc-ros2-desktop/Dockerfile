FROM osrf/ros2:ardent-ros-base

ENV DEBIAN_FRONTEND noninteractive

# build-in packages
RUN apt-get update \
&& apt-get install -y --no-install-recommends software-properties-common curl \
&& sh -c "echo 'deb http://download.opensuse.org/repositories/home:/Horst3180/xUbuntu_16.04/ /' >> /etc/apt/sources.list.d/arc-theme.list" \
&& curl -SL http://download.opensuse.org/repositories/home:Horst3180/xUbuntu_16.04/Release.key | apt-key add - \
&& add-apt-repository ppa:fcwu-tw/ppa \
&& apt-get update \
&& apt-get install -y --no-install-recommends --allow-unauthenticated \
supervisor \
openssh-server pwgen sudo vim-tiny \
net-tools \
lxde x11vnc xvfb \
gtk2-engines-murrine ttf-ubuntu-font-family \
firefox \
nginx \
python-pip python-dev build-essential \
mesa-utils libgl1-mesa-dri \
gnome-themes-standard gtk2-engines-pixbuf gtk2-engines-murrine pinta arc-theme \
dbus-x11 x11-utils \
terminator 

# install ros2 packages
RUN apt-get install -y \
ros-ardent-desktop

# user tools
RUN apt-get install -y \
gedit \
okular \
&& apt-get autoclean \
&& apt-get autoremove \
&& rm -rf /var/lib/apt/lists/*

# tini for subreap
ENV TINI_VERSION v0.9.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /bin/tini
RUN chmod +x /bin/tini

ADD image /
RUN pip install setuptools wheel && pip install -r /usr/lib/web/requirements.txt

RUN cp /usr/share/applications/terminator.desktop /root/Desktop
RUN echo "source /opt/ros/ardent/setup.bash" >> /root/.bashrc

EXPOSE 80
WORKDIR /root
ENV HOME=/home/ubuntu \
SHELL=/bin/bash
ENTRYPOINT ["/startup.sh"]