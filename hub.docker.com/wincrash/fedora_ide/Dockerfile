FROM fedora
MAINTAINER ruslan pacevic
RUN dnf -y install http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-22.noarch.rpm 
RUN dnf -y install http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-22.noarch.rpm 
RUN dnf -y install tar wget nano mc htop which git gcc-c++ make cmake qt-creator glx-utils
RUN dnf -y install xorg-x11-drv-nvidia-340xx
RUN dnf -y install vtk-devel vtk-python vtk-qt vtk-qt-python java-1.8.0-openjdk

VOLUME ["/work"]
VOLUME ["/data"]
EXPOSE 22
EXPOSE 21000
EXPOSE 22000
EXPOSE 80
EXPOSE 8080
EXPOSE 8282
EXPOSE 8484

ADD http://download.jetbrains.com/python/pycharm-community-4.5.3.tar.gz /
RUN tar xzf pycharm-community-4.5.3.tar.gz
RUN dnf -y install qt5-*-devel tcp_wrappers-devel qt5-qttools-static libXt-devel libtiff-devel patch mesa-libGLU-devel libXi-devel

CMD ["/bin/bash"]
