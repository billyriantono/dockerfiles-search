FROM letsbonus/php:7.0

RUN apt-get update && apt-get install -y --no-install-recommends \
    nano \
    openssh-server \
    php7.0-xdebug \
    telnet \
 && rm -rf /var/lib/apt/lists/*

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY xdebug.ini       /etc/php/7.0/mods-available/xdebug.ini
COPY dotbashrc        /root/.bashrc
COPY tooling/*        /usr/local/bin/

# SSHD daemon setup as per the official documentation
# at https://docs.docker.com/engine/examples/running_ssh_service/
RUN mkdir /var/run/sshd \
 && echo 'root:lbmonkey' | chpasswd \
 && sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
 && sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

# FPM child processes run as root
RUN sed -i 's@user = www-data@user = root@' /etc/php/7.0/fpm/pool.d/www.conf \
 && sed -i 's@group = www-data@group = root@' /etc/php/7.0/fpm/pool.d/www.conf \
 && rm /etc/php/7.0/cli/conf.d/20-xdebug.ini

EXPOSE 22 9000
