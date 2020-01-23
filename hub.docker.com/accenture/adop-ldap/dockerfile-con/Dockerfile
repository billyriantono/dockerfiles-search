FROM ubuntu:14.04

ARG DEBIAN_FRONTEND=noninteractive

# Kiuwan patterns
# Revisar los ficheros de configuracion de kiuwan para no usar los strings de host y puertos, usaremos siempre 127.0.0.1 y los puertos estandar

ARG KIUWAN_VOL=${KIUWAN_VOL:-/kiuwan_vol}

# ------------------------------
# Variables Entorno de Ejecucion
# ------------------------------
ENV	NOTVISIBLE="in users profile" \
	ROOT_PWD=${ROOT_PWD:-"nopass"}


ENV KIUWAN_FIRST_TIME=${KIUWAN_FIRST_TIME:-""} \
	START_AND_RUN=${START_AND_RUN:-""}

# -------------------------
# Instalamos software comun
# -------------------------
RUN	apt-get update && \
	apt-get -y install curl wget unzip tzdata locales ntp && \	
	apt-get -y install apt-utils vim supervisor

RUN mkdir -p /var/log/supervisor

# ----------------------------------
# DATE and TIMEZONE: SPANISH, MADRID 
# ----------------------------------

RUN mv /etc/localtime  /etc/localtime.original && \
	ln -s  /usr/share/zoneinfo/Europe/Madrid  /etc/localtime

# Comentamos servidores de ubuntu y ponemos los nuestros
RUN sed -i 's/pool 0/# pool 0/' /etc/ntp.conf && \
	sed -i 's/pool 0/# pool 1/' /etc/ntp.conf && \
	sed -i 's/pool 0/# pool 2/' /etc/ntp.conf && \
	sed -i 's/pool 0/# pool 3/' /etc/ntp.conf

RUN sed -i 's|# Specify one or more NTP servers.|# Specify one or more NTP servers.\nserver hora.roa.es\nserver hora.rediris.es\nserver 1.es.pool.ntp.org\nserver 0.europe.pool.ntp.org\nserver 2.europe.pool.ntp.org|' /etc/ntp.conf

# LOCALE SPANISH
RUN localedef -i es_ES -c -f UTF-8 -A /usr/share/locale/locale.alias es_ES.UTF-8 && \
	echo es_ES.UTF-8 UTF-8 > /etc/locale.gen && \
    locale-gen
	
# --------------
# Openssh-server
# --------------

RUN	apt-get update && \
	apt-get -y install openssh-server
	
# https://jinetedeldragon.wordpress.com/2009/06/22/sed-en-una-linea-sed-one-liners-parte-i/
# Cambiar solo aquella lineas que no contengan setting

RUN sh -c "echo root:${ROOT_PWD:-nopass} |chpasswd" && \
	sed -i -e '/setting/!s|PermitRootLogin without-password|PermitRootLogin yes|' /etc/ssh/sshd_config && \
	sed -i -e 's|#PasswordAuthentication yes|PasswordAuthentication yes|' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
RUN echo "export VISIBLE=now" >> /etc/profile && \	
	mkdir -p /var/run/sshd
	

# -------
# Apache2
# -------
RUN apt-get -y install apache2
# RUN	a2enmod mpm_prefork && \
RUN	a2enmod headers && \
	a2enmod expires && \
	a2enmod rewrite && \
	a2enmod proxy && \
	a2enmod proxy_ajp && \	
	a2enmod proxy_balancer && \	
	a2enmod lbmethod_byrequests && \		
	a2enmod proxy_http && \		
	a2enmod proxy_http && \		
	a2enmod slotmem_shm && \			
	a2enmod socache_shmcb && \				
	a2enmod ssl && \					
	a2enmod unique_id
RUN mkdir /var/lock/apache2 && \
 mkdir /var/run/apache2 && \
 chmod -R 777 /var/lock/apache2 /var/run/apache2

RUN echo "Hola Caracola" > /var/www/html/hola.html

RUN sed -i 's|^# Global configuration|# Global configuration\nServerName miapache\n|' /etc/apache2/apache2.conf  

# kiuwan_vol
# -----------
RUN mkdir -p ${KIUWAN_VOL} && \
	mkdir -p ${KIUWAN_VOL}/logs && \
	mkdir -p ${KIUWAN_VOL}/logs/apache2 && \
	chown -R www-data:www-data ${KIUWAN_VOL}/logs/apache2

# --------
# Arranque
# --------
COPY ./startup.sh /root/startup.sh
RUN chmod +x /root/startup.sh

# -----------
# Supervisord
# -----------
RUN echo "[supervisord]" >> /etc/supervisor/conf.d/0_FIRST_FILE.conf && \
	echo "nodaemon=true" >> /etc/supervisor/conf.d/0_FIRST_FILE.conf
	
# NTPD
RUN	echo "[program:ntpd]" >> /etc/supervisor/conf.d/1_NTPD.conf && \
	echo "command=/usr/sbin/ntpd -u ntp:ntp -p /var/run/ntpd.pid -g -n" >> /etc/supervisor/conf.d/1_NTPD.conf && \
	echo "process_name=%(program_name)s" >> /etc/supervisor/conf.d/1_NTPD.conf && \
	echo "autostart=true" >> /etc/supervisor/conf.d/1_NTPD.conf && \
	echo "autorestart=true" >> /etc/supervisor/conf.d/1_NTPD.conf && \
	echo "user=root" >> /etc/supervisor/conf.d/1_NTPD.conf && \
	echo "directory=/" >> /etc/supervisor/conf.d/1_NTPD.conf && \
	echo "stdout_logfile=/var/log/supervisor_%(program_name)s-stdout.log" >> /etc/supervisor/conf.d/1_NTPD.conf && \
	echo "stderr_logfile=/var/log/supervisor_%(program_name)s-stderr.log" >> /etc/supervisor/conf.d/1_NTPD.conf

# SSHD
RUN	echo "[program:sshd]" >> /etc/supervisor/conf.d/2_SSHD.conf && \
	echo "command=/usr/sbin/sshd -D" >> /etc/supervisor/conf.d/2_SSHD.conf && \
	echo "autorestart=true" >> /etc/supervisor/conf.d/2_SSHD.conf
	
# APACHE2
RUN	echo "[program:apache2]" >> /etc/supervisor/conf.d/9_APACHE2.conf && \
	echo "command=/bin/bash -c \"source /etc/apache2/envvars && exec /usr/sbin/apache2 -DFOOREGROUND\"" >> /etc/supervisor/conf.d/9_APACHE2.conf && \
	echo "stdout_events_enabled=true" >> /etc/supervisor/conf.d/9_APACHE2.conf && \	
	echo "stderr_events_enabled=true" >> /etc/supervisor/conf.d/9_APACHE2.conf && \		
	echo "autostart=true" >> /etc/supervisor/conf.d/9_APACHE2.conf && \	
	echo "autorestart=true" >> /etc/supervisor/conf.d/9_APACHE2.conf

RUN	rm -rf /var/lib/apt/lists/*

VOLUME ${KIUWAN_VOL}	

EXPOSE 80 443

CMD ["/root/startup.sh"]