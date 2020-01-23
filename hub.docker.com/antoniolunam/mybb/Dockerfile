FROM debian:latest

MAINTAINER "Antonio Luna" "equinoxe4@gmail.com"

COPY mybbservice /bin/mybbservice

RUN apt-get update; \
	apt-get install -y apache2 php5 libapache2-mod-php5 php5-mcrypt php5-gd php5-mysql php5-xmlrpc wget unzip; \
	DEBIAN_FRONTEND=noninteractive apt-get install -y mysql-server; \
	apt-get clean; apt-get autoclean
            

RUN wget 'http://resources.mybb.com/downloads/mybb_1806.zip'; \
    rm -rf /var/www/html; \
    unzip mybb_1806.zip -d /var/www/; \
    mv /var/www/Upload /var/www/html; \
    chown -R www-data:www-data /var/www/html; \
    rm -rf /var/www/Documentation; \
    chmod +x /bin/mybbservice; \
    echo "0" > /dbstatus

ENV MYBB_BBDD=mybbdd
ENV MYBB_USER=root
ENV MYBB_PASSWD=root

EXPOSE 80 443

ENTRYPOINT ["/bin/mybbservice"]