# 16.04 car on utilise un version antérieur de php
FROM ubuntu:16.04

# Installation de apache2 , php , mysql ,curl et nano
RUN apt-get update && apt-get -y upgrade && apt-get -y install apache2 php7.0 php7.0-mysql libapache2-mod-php7.0 curl nano

# Copie des fichiers de configuration des sites
ADD https://raw.githubusercontent.com/VareTom/WoodyToys-WT4-/master/DockerWeb/conf/b2b.wt4.ephec-ti.be.conf /etc/apache2/sites-available/b2b.wt4.ephec-ti.be.conf
ADD https://raw.githubusercontent.com/VareTom/WoodyToys-WT4-/master/DockerWeb/conf/intranet.wt4.ephec-ti.be.conf /etc/apache2/sites-available/intranet.wt4.ephec-ti.be.conf

# Creation des dossiers pour les sites
RUN mkdir /var/www/html/b2b.wt4.ephec-ti.be
RUN mkdir /var/www/html/intranet.wt4.ephec-ti.be

# Copie des fichiers des sites situé sur le github
ADD https://raw.githubusercontent.com/VareTom/WoodyToys-WT4-/master/DockerWeb/site/b2b/index.php /var/www/html/b2b.wt4.ephec-ti.be/index.php
ADD https://raw.githubusercontent.com/VareTom/WoodyToys-WT4-/master/DockerWeb/site/int/index.html /var/www/html/intranet.wt4.ephec-ti.be/index.html

# Activer les sites (désactiver celui par défault) 
# Activer des mods pour php
RUN a2dissite 000-default.conf
RUN a2ensite b2b.wt4.ephec-ti.be
RUN a2ensite intranet.wt4.ephec-ti.be
RUN a2enmod php7.0
RUN a2enmod rewrite

# Redemarre apache pour prendre en compte les modifs
RUN /etc/init.d/apache2 restart

# Annonce les ports utilisés
EXPOSE 80 443

CMD apache2ctl -D FOREGROUND

