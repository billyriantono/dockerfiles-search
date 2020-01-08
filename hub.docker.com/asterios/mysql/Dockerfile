FROM mysql:5.6

# Update & upgrade
RUN DEBIAN_FRONTEND=noninteractive apt-get update \
	&& DEBIAN_FRONTEND=noninteractive apt-get install -y locales mc htop ifstat

# Configure timezone and locale
ENV LANGUAGE=en_US.UTF-8 LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 TERM=xterm
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen \
	&& echo "ru_RU.UTF-8 UTF-8" >> /etc/locale.gen \
	&& locale-gen \
	&& dpkg-reconfigure -f noninteractive locales \
	&& unlink /etc/localtime \
	&& echo "Europe/Moscow" > /etc/timezone \
	&& dpkg-reconfigure -f noninteractive tzdata

# Defaults
RUN echo [mysqld] > /etc/mysql/conf.d/customs.cnf \
	&& echo character-set-server	= utf8 >> /etc/mysql/conf.d/customs.cnf \
	&& echo skip-name-resolve >> /etc/mysql/conf.d/customs.cnf \
	&& echo key_buffer_size		= 16M >> /etc/mysql/conf.d/customs.cnf \
	&& echo max_allowed_packet	= 16M >> /etc/mysql/conf.d/customs.cnf \
	&& echo myisam-recover-options	= OFF >> /etc/mysql/conf.d/customs.cnf \
	&& echo max_connections		= 256 >> /etc/mysql/conf.d/customs.cnf
