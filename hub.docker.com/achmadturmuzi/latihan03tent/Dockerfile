# Dockerfile für Joomla 
# acdaic4v 07.08.2015
# Basiert auf grundlegende Perl- Images
FROM acdaic4v/ubuntu-perl-mysql:v20161124
MAINTAINER acdaic4v <acdaic4v@sloervi.de>

# Pakete für die Erstellung von
#	- Grafiken
#	- Excel- Tabellen
#	- Finanzen

RUN apt-get update && apt-get install -y \
        graphviz libgd-gd2-perl \
        libgd2-dev 

RUN cpanm GD \
&&  cpanm Chart::Lines \
&&  cpanm CMS::Joomla \
&&  cpanm Math::Financial \
&&  cpanm Spreadsheet::WriteExcel 

# CPAN- Verzeichnis wieder aufräumen
RUN rm -rf .cpanm

