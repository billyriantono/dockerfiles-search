# this is built on the top of Meng Wang's https://hub.docker.com/r/icebert/ucsc_genome_browser/
FROM ubuntu:16.04
# MAINTAINER Meng Wang <wangm0855@gmail.com>
MAINTAINER Bo Han <bowhan@me.com>
LABEL Description="UCSC Genome Browser"

ARG Genomes="hg38 mm10 rn6 macFas5 dm6"

#
# Install dependencies
#
RUN apt-get update && apt-get install -y git build-essential \
    apache2 mysql-client-5.7 mysql-client-core-5.7 \
    libpng12-dev libssl-dev openssl libmysqlclient-dev && \
    apt-get clean

#
# Get browser source codes
#
ENV MACHTYPE x86_64
RUN mkdir -p ~/bin/${MACHTYPE}
RUN rm /var/www/html/index.html && mkdir /var/www/trash && \
    mkdir /usr/local/apache && ln -s /var/www/html /usr/local/apache/htdocs && \
    rsync -avzP rsync://hgdownload.cse.ucsc.edu/htdocs/ /var/www/html/

RUN mkdir /var/www/cgi-bin && \
    rsync -avP rsync://hgdownload.soe.ucsc.edu/cgi-bin/ /var/www/cgi-bin/

#
# Config db connection
#
RUN {  \
    echo "gbdbLoc1=/data/gbdb/"; \
    echo "gbdbLoc2=http://hgdownload.cse.ucsc.edu/gbdb/"; \
    echo "db.trackDb=trackDb"; \
    echo "db.host=gbdb"; \
    echo "db.user=admin"; \
    echo "db.password=admin"; \
    echo "db.socket=/var/run/mysqld/mysqld.sock"; \
    echo "slow-db.host=genome-mysql.cse.ucsc.edu"; \
    echo "slow-db.user=genomep"; \
    echo "slow-db.password=password"; \
    echo "central.db=hgcentral"; \
    echo "central.host=gbdb"; \
    echo "central.user=admin"; \
    echo "central.password=admin"; \
    echo "central.domain="; \
    echo "backupcentral.db=hgcentral"; \
    echo "backupcentral.host=gbdb"; \
    echo "backupcentral.user=admin"; \
    echo "backupcentral.password=admin"; \
    echo "backupcentral.domain="; \
} > /var/www/cgi-bin/hg.conf 


#
# Config daliy clean
#
RUN { \
        echo '#!/bin/bash'; \
        echo 'find /var/www/trash/ \! \( -regex "/var/www/trash/ct/.*" \
              -or -regex "/var/www/trash/hgSs/.*" \) -type f -amin +5040 -exec rm -f {} \;'; \
        echo 'find /var/www/trash/    \( -regex "/var/www/trash/ct/.*" \
              -or -regex "/var/www/trash/hgSs/.*" \) -type f -amin +10080 -exec rm -f {} \;'; \
    } > /etc/cron.daily/genomebrowser

RUN chmod +x /etc/cron.daily/genomebrowser

#
# Config apache
#
RUN sed -i 's/<\/VirtualHost>//' /etc/apache2/sites-enabled/000-default.conf && \
    { \
        echo 'XBitHack on'; \
        echo ''; \
        echo '<Directory /var/www/html>'; \
        echo '    Options +Includes'; \
        echo '    SSILegacyExprParser on'; \
        echo '</Directory>'; \
        echo ''; \
        echo 'ScriptAlias /cgi-bin/ /var/www/cgi-bin/'; \
        echo '<Directory "/var/www/cgi-bin">'; \
        echo '    AllowOverride None'; \
        echo '    Options +ExecCGI -MultiViews +SymLinksIfOwnerMatch'; \
        echo '    SetHandler cgi-script'; \
        echo '    Require all granted'; \
        echo '</Directory>'; \
        echo ''; \
        echo '<Directory /var/www/html/trash>'; \
        echo '    Options MultiViews'; \
        echo '    AllowOverride None'; \
        echo '    Order allow,deny'; \
        echo '    Allow from all'; \
        echo '</Directory>'; \
        echo ''; \
        echo '</VirtualHost>'; \
    } >> /etc/apache2/sites-enabled/000-default.conf

RUN ln -s /etc/apache2/mods-available/include.load /etc/apache2/mods-enabled/ && \
    ln -s /etc/apache2/mods-available/cgi.load /etc/apache2/mods-enabled/


#
# Get gbdb data from UCSC
#

RUN for genome in ${Genomes}; do \
        mkdir -p /gbdb/visiGene /gbdb/${genome} \
        && rsync -avP  --include "known*" --include "*2bit" --exclude "*" rsync://hgdownload.cse.ucsc.edu/gbdb/${genome}/  /gbdb/${genome}/; \
    done

RUN chown -R www-data.www-data /var/www /gbdb

#
# Start apache
#
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

EXPOSE 80 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]