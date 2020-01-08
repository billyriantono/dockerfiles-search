FROM ubuntu

LABEL maintainer="mfpjayb@gmail.com"

RUN apt-get update && apt-get -y upgrade

ENV TZ=America/Los_Angeles
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN DEBIAN_FRONTEND=noninteractive

RUN apt-get install -y software-properties-common

RUN apt-get -y install nginx curl tmux git screen

# added git config
RUN git config --global user.email "darius.bualan@intechsive.com"
RUN git config --global user.name "Darius Bualan"

# Install Mongodb
RUN apt-get install -y mongodb
RUN mkdir /data
RUN mkdir /data/db
RUN rm -f /var/lib/mongodb/mongod.lock
RUN mongod --repair

# Install Apache
# RUN apt-get install apache2

# Install PHP
RUN apt-get install -y php7.2 libapache2-mod-php7.2 php7.2-curl php7.2-cli php7.2-common php7.2-json php7.2-mysql php7.2-readline php7.2-mbstring php7.2-xml php7.2-gd php7.2-zip

# Install Mysql
RUN apt-get install -y mysql-server-5.7 mysql-client-5.7 mysql-client-core-5.7 mysql-common
RUN usermod -d /var/lib/mysql/ mysql

# Install Python
RUN apt-get install -y python3.7

# Install Composer
RUN apt-get install -y composer

# Install Nodejs
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs build-essential

# Install Redis
RUN apt-get install -y redis

# Install Angular Cli and Firebase
RUN npm install -g @angular/cli firebase-tools

# Install Neovim
RUN add-apt-repository ppa:neovim-ppa/stable
RUN apt-get update
RUN apt-get install -y neovim
RUN update-alternatives --install /usr/bin/vi vi /usr/bin/nvim 60
RUN update-alternatives --config vi
RUN update-alternatives --install /usr/bin/vim vim /usr/bin/nvim 60
RUN update-alternatives --config vim
RUN update-alternatives --install /usr/bin/editor editor /usr/bin/nvim 60
RUN update-alternatives --config editor

ENV TERM xterm-256color

RUN apt-get install -y libpng-dev

# Nginx volume
VOLUME /usr/share/nginx/html

# Mysql db data
VOLUME /var/lib/mysql

# Mongo db data
VOLUME /data/db

EXPOSE 80
EXPOSE 3000 
EXPOSE 8000 

# ng serve port
EXPOSE 4200 

# mysql port
EXPOSE 3306

# redis port
EXPOSE 6379

CMD ["bash", "-l"]

