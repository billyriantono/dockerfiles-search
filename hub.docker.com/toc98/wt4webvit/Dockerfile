FROM ubuntu:16.04

# Installation de apache2 , php , mysql , nano et curl
RUN apt-get update && apt-get -y upgrade && apt-get -y install apache2 curl nano 

# Copie des fichiers de configuration des sites
ADD https://raw.githubusercontent.com/VareTom/WoodyToys-WT4-/master/DockerWebVit/conf/www.wt4.ephec-ti.be.conf /etc/apache2/sites-available/www.wt4.ephec-ti.be.conf

# Creation des dossiers pour les sites
RUN mkdir /var/www/html/www.wt4.ephec-ti.be

# Copie des fichiers des sites
ADD https://raw.githubusercontent.com/VareTom/WoodyToys-WT4-/master/DockerWebVit/site/index.html /var/www/html/www.wt4.ephec-ti.be/index.html

# Activer site et mods
RUN a2dissite 000-default.conf
RUN a2ensite www.wt4.ephec-ti.be
RUN a2enmod rewrite

# Redémarre apache pour prendre en compte les modifications
RUN /etc/init.d/apache2 restart

# Annonce les ports utilisés
EXPOSE 80 443

CMD apache2ctl -D FOREGROUND

