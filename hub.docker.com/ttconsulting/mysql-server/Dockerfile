FROM ttconsulting/apache-php-5.4-server:latest

RUN yum install -y mariadb-server openssh-server supervisor

VOLUME ['/etc/mysql', '/var/lib/mysql', '/etc/ssh', '/var/run/supervisor']

#change root password
RUN usermod -p '$6$9ID2aCm8$6lGDQzTqYxTX6rGBrADQICZt.eIWchWHPD.yOB1.YeKy3ty0E9d7B1jYEcZVsuCa9NjKu1BOzd4GkC7FP92OA/' root

WORKDIR /root

ENTRYPOINT supervisord -c /var/run/supervisor/run.conf
