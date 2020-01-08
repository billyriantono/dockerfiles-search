FROM mwaeckerlin/apache
MAINTAINER mwaeckerlin

RUN apt-get update && apt-get install -y graphite-web apache2 libapache2-mod-wsgi
RUN a2dissite 000-default
RUN cp /usr/share/graphite-web/apache2-graphite.conf /etc/apache2/sites-available
RUN a2ensite apache2-graphite

ADD start.sh /start.sh

CMD /start.sh

VOLUME /var/lib/graphite
