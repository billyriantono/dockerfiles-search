FROM debian:8

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y wget vim
RUN cd /root && wget https://www.dotdeb.org/dotdeb.gpg && apt-key add dotdeb.gpg
RUN echo "deb http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list
RUN echo "deb-src http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list
RUN echo "deb http://ftp.bg.debian.org/debian/ jessie main contrib non-free" >> /etc/apt/sources.list
RUN echo "deb-src http://ftp.bg.debian.org/debian/ jessie main contrib non-free" >> /etc/apt/sources.list
RUN apt-get update 

RUN apt-get install -y php7.0-cgi php7.0-xml php7.0-mysql php7.0-mbstring git unzip curl apache2 libapache2-mod-fastcgi apache2-mpm-worker apache2-suexec libapache2-mod-fcgid
RUN a2enmod actions fastcgi rewrite

RUN wget "https://getcomposer.org/download/1.3.0/composer.phar" -q -O /bin/composer && chmod +x /bin/composer

CMD /etc/init.d/apache2 restart && tail -f /var/log/apache2/error.log
