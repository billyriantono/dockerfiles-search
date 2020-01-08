FROM ubuntu
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update
RUN apt-get install apt-utils -y
RUN apt-get install mariadb-server -y
RUN apt-get install apache2 -y
RUN apt-get install php php-mysql -y
COPY wordpress.tar.gz /var/www/html
WORKDIR /var/www/html
RUN tar -zxvf wordpress.tar.gz
RUN mkdir /info
COPY read.txt /info
COPY wp-config.php /info
WORKDIR /info
EXPOSE 3306
EXPOSE 80
