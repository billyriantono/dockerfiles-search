FROM centos:7.6.1810
RUN yum -y update
RUN yum -y install libreoffice-base libreoffice-calc libreoffice-writer java-11-openjdk
RUN alternatives --set java java-11-openjdk.x86_64
RUN yum -y install epel-release
RUN yum -y install curl cabextract xorg-x11-font-utils fontconfig
RUN rpm -i https://downloads.sourceforge.net/project/mscorefonts2/rpms/msttcore-fonts-installer-2.6-1.noarch.rpm
CMD ["/bin/bash"]