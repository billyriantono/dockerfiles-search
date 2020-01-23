FROM ubuntu:14.04.3
MAINTAINER alateam <team@ala-it.com>

##################### 常用文件夹准备
RUN mkdir /workspace /tools /runner /temp /me
ENV DEBIAN_FRONTEND noninteractive

###########ADD safe user
RUN useradd -m -u 600 safe

##################### 更新系统
RUN apt-get update

##################### 常用工具
RUN apt-get -y install gcc make build-essential curl wget vim openssl unzip python git mysql-client

##################### install oh-my-zsh
RUN apt-get -y install zsh
RUN git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
RUN cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
RUN chsh -s /bin/zsh

##############install nvm
ENV HOME /root
ENV PATH /root/.nvm/v0.10.36/bin:$PATH
RUN git clone https://github.com/creationix/nvm.git $HOME/.nvm
RUN pwd $HOME/.nvm/


##############install node
RUN bash -c '. $HOME/.nvm/nvm.sh; nvm install 0.10.36 && nvm alias default 0.10.36'
#########install pm2
Run npm install pm2 -g



############install php
RUN apt-get -y install php5-fpm php5-cli php5-mysql php5-mcrypt php5-gd php-pear php-apc php5-curl  php5-sqlite
RUN php5enmod mcrypt


############install composer and laravel
RUN  curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer


#######add other base environment
##RUN apt-get install -y build-essential g++ curl libssl-dev apache2-utils git libxml2-dev sshfs

########C9
RUN echo 'update C9'
RUN cd /tools && git clone https://github.com/c9/core.git cloud9
WORKDIR /tools/cloud9
RUN git pull origin master
#RUN git pull origin c9
RUN chmod 755 scripts/*.sh
RUN scripts/install-sdk.sh

# Tweak standlone.js conf
RUN sed -i -e 's_127.0.0.1_0.0.0.0_g' /tools/cloud9/configs/standalone.js

######### intall nginx and php
RUN apt-get -y install nginx 
RUN echo "cgi.fix_pathinfo = 0;" >> /etc/php5/fpm/php.ini
ADD etc/vhost/default.conf /etc/nginx/sites-available/default

RUN mkdir -p /workspace/logs/nginx


#安装phpmyadmin
RUN wget https://files.phpmyadmin.net/phpMyAdmin/4.5.2/phpMyAdmin-4.5.2-all-languages.tar.gz -O - | tar -xz
RUN mv phpMyAdmin* /phpmyadmin
ADD etc/phpmyadmin.config.inc.php /phpmyadmin/config.inc.php
ADD etc/vhost/phpmyadmin.conf /etc/nginx/sites-available/phpmyadmin
RUN ln -s /etc/nginx/sites-available/phpmyadmin /etc/nginx/sites-enabled/phpmyadmin

RUN apt-get -y install openssh-server

EXPOSE 80 81 82 22 21 20 8080 8081 8082 8083

WORKDIR /runner
ADD run.sh run.sh
RUN chmod 755 *.sh
CMD ["./run.sh"]


