FROM        phusion/baseimage
MAINTAINER  Geert

ENV         HOME=/home
ENV         LANG en_US.UTF-8
ENV         WEBMIN_VERSION=1.770
ENV         config_dir=/webmin-data/config
ENV         var_dir=/webmin-data/var
RUN         locale-gen en_US.UTF-8

# Install packages
RUN         apt-get update &&\
                apt-get install -y wget perl libnet-ssleay-perl openssl \
                    libauthen-pam-perl libpam-runtime libio-pty-perl \
                    python

ADD         create_default_config_webmin.sh /create_default_config_webmin.sh
ADD         create_default_config_user.sh /create_default_config_user.sh

RUN         wget "http://prdownloads.sourceforge.net/webadmin/webmin-${WEBMIN_VERSION}-minimal.tar.gz" -P /tmp/ &&\
                tar xvf "/tmp/webmin-${WEBMIN_VERSION}-minimal.tar.gz" -C /tmp &&\
                ls -al /tmp

RUN         mv "/tmp/webmin-${WEBMIN_VERSION}" /webmin-install &&\
                rm -rf /tmp/* &&\
                mkdir /webmin &&\
                mkdir -p "${config_dir}" &&\
                mkdir -p "${var_dir}" &&\
                cd /webmin-install &&\
                ./setup.sh /webmin &&\
                wget https://raw.githubusercontent.com/qooob/authentic-theme/master/.build/authentic-theme-latest.wbt.gz &&\
                perl ./install-module.pl ./authentic-theme-latest.wbt.gz "${config_dir}" &&\
                sed -i 's/ssl=0/ssl=1/g' "${config_dir}"/miniserv.conf &&\
                sed -i 's/admin:/root:/g' "${config_dir}"/miniserv.users &&\
                sed -i 's/admin:/root:/g' "${config_dir}"/webmin.acl &&\
                echo "preroot=authentic-theme" >> "${config_dir}"/miniserv.conf &&\
                echo "nofork=1" >> "${config_dir}"/miniserv.conf &&\
                echo "theme=authentic-theme" >> "${config_dir}"/config &&\
                /create_default_config_webmin.sh &&\
                /create_default_config_user.sh

ADD         start_webmin.sh /etc/service/webmin/run
ADD         01_user_setup.sh /etc/my_init.d/01_user_setup.sh
ADD         02_webmin_setup.sh /etc/my_init.d/02_webmin_setup.sh
ADD         user_cron.sh /etc/cron.hourly/user_cron.sh

EXPOSE      10000

VOLUME      /webmin-data
VOLUME      /user-data

# Use baseimage-docker's init system.
CMD         ["/sbin/my_init"]
