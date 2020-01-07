FROM eclipse/php

RUN sudo apt-get update && \
    sudo apt-get install php7.0-zip php7.0-ldap vim -y && \
    sudo apt-get -y clean && \
    sudo rm -rf /var/lib/apt/lists/*

#Disable directory listing
RUN sudo sed -i 's/Options Indexes FollowSymLinks/Options FollowSymLinks/g'  /etc/apache2/apache2.conf
COPY php7.0.conf /etc/apache2/mods-available/php7.0.conf
