FROM ruby:2.5
RUN apt update
RUN wget http://dev.mysql.com/get/mysql-apt-config_0.8.9-1_all.deb
RUN apt install -y lsb-release
RUN dpkg -i mysql-apt-config_0.8.9-1_all.deb
RUN apt update
RUN apt install -y mysql-server
RUN mysql --version
RUN apt install -y redis-server
RUN apt install -y phantomjs
