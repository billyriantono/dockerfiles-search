FROM ubuntu:16.04

ENV LANG=en_US.UTF-8 LANGUAGE=en_US.UTF-8 LC_ALL=en_US.UTF-8
ENV TZ=Asia/Jakarta
ENV VARNISH_HOST=127.0.0.1
ENV VARNISH_BACKEND_PORT=8080
ENV USER=appuser

# general
RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install software-properties-common python-software-properties sudo git curl nano wget net-tools locales
RUN locale-gen en_US.UTF-8

# set timezone
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN apt-get install -y tzdata
RUN dpkg-reconfigure tzdata 

# varnish
RUN apt-get install -y varnish
ADD etc/varnish/default.vcl /etc/varnish/default.vcl
ADD etc/default/varnish /etc/default/varnish
RUN sed -i 's/VARNISH_HOST/${VARNISH_HOST}/g' /etc/varnish/default.vcl
RUN sed -i 's/VARNISH_PORT/${VARNISH_BACKEND_PORT}/g' /etc/varnish/default.vcl
RUN sed -i 's/:6081/:80/g' /lib/systemd/system/varnish.service

# create docker group and user
RUN useradd -rm -d /home/$USER -s /bin/bash -G sudo -u 1001 $USER
ADD etc/sudoers /etc/sudoers

# add entrypoint
ADD entrypoint.sh /opt/entrypoint.sh
RUN chmod +x /opt/entrypoint.sh

USER $USER
WORKDIR /home/$USER

EXPOSE 80 6082
ENTRYPOINT [ "/bin/bash" , "/opt/entrypoint.sh"]