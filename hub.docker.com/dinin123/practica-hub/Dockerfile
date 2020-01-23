FROM debian:jessie
MAINTAINER dinin1@gmail.com


RUN     apt-get update && apt-get upgrade \ 

        # Instalar SSL
        && apt-get -y install openssl \
        # 
        # Instalar Apache
        # 
        && apt-get -y install apache2 apache2-doc \
        #
        # Instalar PHP y MODs
        #
        && apt-get -y install php5-common libapache2-mod-php5 php5-cli php5-common php5-curl php5-gd php5-mysql php5-mcrypt \

        # Borramos Basura
        && apt-get clean && rm -rf /var/lib/apt/lists/*

        # LOG A PANTALLA
RUN     ln -sf /dev/stdout /var/log/apache2/access.log && ln -sf /dev/stderr /var/log/apache2/error.log

ENTRYPOINT ["/usr/sbin/apachectl","-D","FOREGROUND"]


EXPOSE 80 443
