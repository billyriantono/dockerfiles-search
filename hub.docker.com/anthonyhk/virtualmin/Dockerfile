FROM ubuntu:bionic
LABEL maintainer="Anthony Astley Lim <anthony.lim@protonmail.com>"
LABEL version="1.0"

ARG DEBIAN_FRONTEND=noninteractive

RUN sed -i 's#exit 101#exit 0#' /usr/sbin/policy-rc.d 
RUN rm  /etc/apt/apt.conf.d/docker-gzip-indexes \ 
    &&  apt-get -o Acquire::GzipIndexes=false update -y \
    &&  apt-get upgrade -y

# Fixes issue with running systemD inside docker builds 
# From https://github.com/gdraheim/docker-systemctl-replacement
COPY systemctl.py /usr/bin/systemctl.py
RUN chmod +x /usr/bin/systemctl.py \
    && cp -f /usr/bin/systemctl.py /usr/bin/systemctl

WORKDIR /tmp

RUN apt-get -y --no-install-recommends -f install wget perl apt-utils \
                ca-certificates apt-transport-https lsb-release ntpdate openssl nano \
                curl screen bind9 bind9-host dnsutils dovecot-common dovecot-imapd \
                openssh-server fail2ban shorewall ruby apache2 quota \
                libcrypt-ssleay-perl unzip zip rsyslog \
                software-properties-common language-pack-en \
                dovecot-pop3d postfix procmail postgrey clamav opendkim
RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN sh -c 'echo "deb https://packages.sury.org/php/ stretch main" > /etc/apt/sources.list.d/php.list'
RUN apt-get update && apt-get upgrade -y

RUN LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php -y && add-apt-repository ppa:adiscon/v8-stable -y 
RUN apt-get update && apt-get upgrade -y

RUN apt-get install -y spamc spamassassin

RUN apt-get install -y -f --no-install-recommends php7.3-cli php7.3-curl php7.3-intl php7.3-json \
        php7.3-mbstring php7.3-mysql php7.3-opcache php7.3-readline php7.3-xml php7.3-xsl \
        php7.3-zip php7.3-bz2 libapache2-mod-php7.3 php7.3 \
        php7.3 php7.3-cgi php7.3-fpm php-memcache php-memcached mysql-common \
        default-libmysqlclient-dev libfreetype6-dev libpng-dev zlib1g-dev libzip-dev imagemagick \
        php7.3-mysql  php7.3-gd libmagickcore-6.q16-3-extra libpng-tools

RUN wget http://www.webmin.com/jcameron-key.asc -qO - | apt-key add -
RUN echo "deb http://download.webmin.com/download/repository sarge contrib" >> /etc/apt/sources.list
RUN wget http://software2.virtualmin.com/lib/RPM-GPG-KEY-virtualmin-6 -qO - | apt-key add - 
RUN echo "deb http://software.virtualmin.com/vm/6/gpl/apt virtualmin-bionic main" >> /etc/apt/sources.list 
RUN echo "deb http://software.virtualmin.com/vm/6/gpl/apt virtualmin-universal main" >> /etc/apt/sources.list 
RUN wget -q http://download.webmin.com/download/virtualmin/webmin-virtual-server-theme_9.3_all.deb 
RUN wget -q http://download.webmin.com/download/virtualmin/webmin-virtual-server_6.07.gpl_all.deb 
RUN apt-get update 
RUN apt-get -y -f install webmin usermin jailkit
RUN dpkg -i webmin-virtual-server_6.07.gpl_all.deb 
RUN apt-get install -f 
RUN dpkg -i webmin-virtual-server-theme_9.3_all.deb 
RUN apt-get install -f 
RUN apt-get dist-upgrade -y 
RUN apt-get autoremove -y 
RUN apt-get clean
RUN rm webmin-virtual-server_6.07.gpl_all.deb 
RUN rm webmin-virtual-server-theme_9.3_all.deb 
RUN rm -rf /var/lib/apt/lists/*


COPY postfix.main.cf /etc/postfix/main.cf
COPY postfix.master.cf /etc/postfix/master.cf    
COPY shorewall.zones /etc/shorewall/zones
COPY shorewall.interfaces /etc/shorewall/interfaces   
COPY shorewall.policy /etc/shorewall/policy
COPY shorewall.rules /etc/shorewall/rules
COPY opt-sysinit.sh /opt/sysinit.sh

# RUN apt-get update 
RUN chmod +x /etc/init.d/dovecot \
    && chmod +x /opt/sysinit.sh \
    && chmod 6711 /usr/bin/procmail \
    && chown root:root /usr/bin/procmail \
    && chown -R postfix:postdrop /var/spool/postfix \
    && touch /etc/postfix/dependent.db /var/log/auth.log /var/log/fail2ban.log \
    && echo "/bin/false" >> /etc/shells \
    && sed -i 's/SetHandler/#SetHandler/' /etc/apache2/mods-available/php7.3.conf
    
RUN systemctl enable shorewall.service rsyslog.service sshd.service fail2ban.service dovecot.service cron.service bind9.service opendkim.service postfix.service apache2.service postgrey.service usermin.service webmin.service
RUN echo "root:virtualmin" | chpasswd
RUN touch /etc/network/interfaces
    
EXPOSE 80 443 21 25 110 143 465 587 993 995 10000 20000 53/udp 53/tcp

VOLUME [ "/var/www/html" ]

WORKDIR /var/www/html

ENTRYPOINT ["bash", "-c", "/opt/sysinit.sh"]
