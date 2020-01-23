FROM debian:squeeze

ENV DEBIAN_FRONTEND noninteractive
ADD sources.list /etc/apt/sources.list
ADD apt.conf /etc/apt/apt.conf
RUN apt-get update && apt-get install -y wget && apt-get clean
RUN wget http://repos.zend.com/zend.key -O- |apt-key add -
RUN groupadd zend && useradd zend -g zend && apt-get update && apt-get install -y aptitude && apt-get clean && aptitude install -y zend-server-ce-php-5.3 && apt-get clean && touch /var/log/apache2/other_vhosts_access.log && apt-get remove -y aptitude

CMD /etc/init.d/zend-server start && tail -f /var/log/apache2/access.log
