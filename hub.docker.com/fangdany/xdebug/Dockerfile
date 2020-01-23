FROM php:7.0-fpm

# 安装常用工具
RUN apt update; \
	apt install vim net-tools iputils-ping htop iotop curl git zip procps wget sudo lsof telnet -y; \
	rm -rf /var/lib/apt/lists/*
# 启用 ll 
RUN php -r '$bashrc="/root/.bashrc";file_put_contents($bashrc,str_replace("# alias ll","  alias ll",file_get_contents($bashrc)));'

# 修改 php-fpm 配置
RUN sed -i 's/\;pid = run\/php-fpm.pid/  pid = run\/php-fpm.pid/g' /usr/local/etc/php-fpm.conf; \
	sed -i 's/\;error_log = log\/php-fpm.log/  error_log = log\/php-fpm.log/g' /usr/local/etc/php-fpm.conf; \
	sed -i 's/\; process.max = 128/  process.max = 128/g' /usr/local/etc/php-fpm.conf; \
	sed -i 's/pm.max_children = 5/pm.max_children = 25/g' /usr/local/etc/php-fpm.d/www.conf; \
	sed -i 's/pm.start_servers = 2/pm.start_servers = 10/g' /usr/local/etc/php-fpm.d/www.conf; \
	sed -i 's/pm.min_spare_servers = 1/pm.min_spare_servers = 5/g' /usr/local/etc/php-fpm.d/www.conf; \
	sed -i 's/pm.max_spare_servers = 3/pm.max_spare_servers = 15/g' /usr/local/etc/php-fpm.d/www.conf; 

RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini

# 安装 xdebug
RUN pecl install xdebug; \
	docker-php-ext-enable xdebug; \
	rm -rf /tmp/pear;\
	{ \
		echo 'xdebug.overload_var_dump=0'; \
		echo 'xdebug.remote_enable=1'; \
		echo 'xdebug.remote_autostart=1'; \
		echo 'xdebug.remote_port=9001'; \
		echo 'xdebug.remote_host=127.0.0.1'; \
		echo '; Effective only in the Linux Environment and docker run option --net=host'; \
		echo '; xdebug.remote_connect_back=1'; \
	} | tee -a /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
# 启用 opcache
RUN docker-php-ext-enable opcache; \
	{ \
		echo 'opcache.revalidate_freq=0'; \
		echo 'opcache.validate_timestamps=10'; \
		echo 'opcache.max_accelerated_files=7963'; \
		echo 'opcache.memory_consumption=192'; \
		echo 'opcache.interned_strings_buffer=16'; \
		echo 'opcache.fast_shutdown=1'; \
	} | tee -a /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini

# 安装依赖与扩展
RUN	requirements="libmcrypt-dev libcurl4-gnutls-dev libpng-dev zlib1g-dev"; \ 	
	apt update; apt install -y $requirements; rm -rf /var/lib/apt/lists/*; \
	docker-php-ext-install -j$(nproc) \
		gd bcmath pdo_mysql mcrypt  pcntl sockets zip; 

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer && \
    composer self-update && \
    composer config -g repo.packagist composer https://packagist.phpcomposer.com

# 安装 igbinary redis
RUN apt update; apt install -y redis-server; rm -rf /var/lib/apt/lists/*; \
	pecl install igbinary redis; \
	yes | pecl install redis; \
	docker-php-ext-enable igbinary redis; \
	rm -rf /tmp/pear; \
	sed -i 's/session.save_handler = files/session.save_handler = redis/g' /usr/local/etc/php/php.ini; \
	sed -i 's/\;session.save_path = "\/tmp"/session.save_path = "tcp:\/\/127.0.0.1:6379"/g' /usr/local/etc/php/php.ini


# 安装 imap bz2
RUN apt update; apt install -y libc-client-dev libkrb5-dev libbz2-dev; rm -r /var/lib/apt/lists/*; \
	docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install imap bz2;\
	rm -rf /tmp/pear

# 安装 tideways
RUN echo 'deb http://s3-eu-west-1.amazonaws.com/tideways/packages debian main' > /etc/apt/sources.list.d/tideways.list; \
	apt update; apt install -y gnupg ;\
	wget -qO - https://s3-eu-west-1.amazonaws.com/tideways/packages/EEB5E8F4.gpg | sudo apt-key add -; \
	apt update; apt install tideways-php; rm -rf /var/lib/apt/lists/*; \
	docker-php-ext-enable tideways

# 安装 tideways_xhprof
RUN cd /usr/local/src; \
	git clone https://github.com/tideways/php-xhprof-extension.git; \
	cd php-xhprof-extension/ ;\
	phpize; \
	./configure; \
	make; \ 
	make install; \
	docker-php-ext-enable tideways_xhprof

# 安装 xlswriter（一个超级强的 EXCEL 导出库）
RUN pecl install xlswriter; \
	docker-php-ext-enable xlswriter

# 安装 mongodb
RUN pecl install mongodb; docker-php-ext-enable mongodb; rm -rf /tmp/pear

# 安装 nginx
RUN apt update; apt install nginx -y; rm -rf /var/lib/apt/lists/*

# 安装 sshd
RUN apt update; apt install -y openssh-server; rm -rf /var/lib/apt/lists/*; \
	mkdir -p /var/run/sshd;\
	echo 'root:root' | chpasswd;\
	sed -i 's/\#PermitRootLogin/PermitRootLogin/' /etc/ssh/sshd_config;\
	sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config


	
# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

# ENV NOTVISIBLE "in users profile"
# RUN echo "export VISIBLE=now" >> /etc/profile

WORKDIR /codes

# php-fpm xdebug
EXPOSE 9000 80 443 22

