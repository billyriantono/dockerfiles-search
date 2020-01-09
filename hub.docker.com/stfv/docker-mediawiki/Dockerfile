FROM mediawiki:lts
MAINTAINER Christof Spies <christof.spies@stfv-koeln.de>

# Enable apache mods.
RUN a2enmod rewrite

# Install VisualEditor
WORKDIR /var/www/html

RUN git clone -b REL1_31 https://gerrit.wikimedia.org/r/p/mediawiki/extensions/VisualEditor.git ./extensions/VisualEditor

WORKDIR /var/www/html/extensions/VisualEditor

RUN git submodule update --init

WORKDIR /var/www/html

COPY config/* /var/www/html/