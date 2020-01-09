FROM debian

RUN apt-get update
RUN apt-get install php7.0 php7.0-cli php7.0-curl php7.0-gd php7.0-mbstring php7.0-soap php7.0-xml git --yes -q

RUN useradd fritz -m
RUN su  fritz 
WORKDIR /home/fritz/

RUN su fritz -c 'git clone https://github.com/BlackSenator/carddav2fb_XR.git'
WORKDIR /home/fritz/carddav2fb_XR

RUN php --ini
RUN apt-get install zip unzip php7.0-zip --yes -q
RUN php --ini
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('SHA384', 'composer-setup.php') ===  '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
RUN su fritz -c 'composer install -d /home/fritz/carddav2fb_XR/'
RUN mkdir /home/fritz/cache
RUN mkdir /home/fritz/carddav2fb_XR/fonpix
#RUN mkdir /media/fritzbox/FRITZ/mediabox/ -r

COPY crontab /var/spool/cron/crontabs/root

RUN apt-get install cron --yes -q
#COPY config.php /home/fritz/config/
#RUN  php /home/fritz/carddav2fb_XR/carddav2fb.php run -c /home/fritz/config/config.php -i

VOLUME /home/fritz/config

CMD ["crond", "-f", "-l", "0", "-d", "0"]
