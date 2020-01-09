FROM unigeocloud/centos-xfce-vnc-novnc:latest
MAINTAINER UniGeoCloud "sgi@unigeocloud.com"

ENV DISPLAY :1
ENV VNC_COL_DEPTH 24
ENV VNC_RESOLUTION 1280x720
ENV VNC_PW abcABC123
ENV VNC_PORT 5901
ENV NOVNC_PORT 6901

############### miniconda installation ####
RUN yum install gcc gcc-c++ bzip2 libxslt-devel freetype-devel libpng-devel libX11-devel lapack-devel blas-devel libsamplerate-devel -y;
RUN yum install python-pip python-devel PyQt4 -y;

############## mysql #######################
RUN yum install http://repo.mysql.com/yum/mysql-5.6-community/el/7/x86_64/mysql-community-release-el7-5.noarch.rpm -y;
RUN yum install mysql-server mysql-devel -y;

############## database schema ############
ADD mysql /var/lib/mysql
RUN chown mysql:mysql -R /var/lib/mysql/*;

############# desktop ####################
RUN echo "${VNC_PW}" | /usr/bin/vncpasswd -f > /home/unigeo/.vnc/passwd 2>/dev/null;
ADD .config/MSNoise.desktop /home/unigeo/Desktop/MSNoise.desktop
RUN chmod +x /home/unigeo/Desktop/MSNoise.desktop;
RUN chown unigeo:unigeo /home/unigeo/Desktop/*

############ MSNoise ####################
RUN pip install numpy;
RUN pip install traitsui traits obspy click mysql-python scikits.samplerate msnoise;

ADD db.ini /home/unigeo/db.ini

############ VNC-noVNC startup script
ADD scripts/ /root/scripts
RUN chmod +x /root/scripts/vnc_novnc_startup.sh;

EXPOSE 5901
EXPOSE 6901

CMD ["/bin/bash"]
