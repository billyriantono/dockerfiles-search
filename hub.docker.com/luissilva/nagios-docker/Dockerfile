FROM ubuntu:16.04

# Envs
ENV NAGIOS_FQDN=nagios.local

# Install Nagios and required software
RUN apt-get update && \
    apt-get install -y net-tools iputils-ping sudo && \
    apt-get update -y && \
    apt-get install -y wget unzip daemon build-essential apache2 php7.0-gd libgd2-xpm-dev libapache2-mod-php7.0 apache2-utils systemd nano nagios-nrpe-plugin openssl libssl-dev unzip systemd && \
    cd /mnt/ && \
    wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.3.4.tar.gz && \
    wget https://nagios-plugins.org/download/nagios-plugins-2.2.1.tar.gz#_ga=2.75789525.1354305546.1521451245-1614901165.152119776 && \
    tar zxvf nagios-4.3.4.tar.gz && \
    tar zxvf nagios-plugins-2.2.1.tar.gz && \
    cd nagios-4.3.4 && \
    useradd nagios && \
    groupadd nagcmd && \
    usermod -a -G nagcmd nagios && \
    usermod -a -G nagcmd www-data && \
    ./configure --with-nagios-group=nagios --with-command-group=nagcmd --with-mail=/usr/bin/mail && \
    make all && make install && \
    make install-init && \
    make install-config && \
    make install-commandmode && \
    /usr/bin/install -c -m 644 sample-config/httpd.conf /etc/apache2/sites-enabled/nagios.conf && \
    a2enmod cgi && \
    a2enmod rewrite && \
    service apache2 restart && \
    cd /mnt/nagios-plugins-2.2.1 && \
    ./configure --with-nagios-user=nagios --with-nagios-group=nagios && \
    make && make install && \
    htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin && \
    ln -s /etc/init.d/nagios /etc/systemd/system/multi-user.target.wants/nagios.service && \
    sed -i 's@#cfg_dir=/usr/local/nagios/etc/servers@cfg_dir=/usr/local/nagios/etc/servers@g' /usr/local/nagios/etc/nagios.cfg && \
    mkdir /usr/local/nagios/etc/servers && \
    sed -i '133,147d' /usr/local/nagios/etc/objects/localhost.cfg

COPY commands.cfg /usr/local/nagios/etc/objects/commands.cfg

COPY linux.cfg /usr/local/nagios/etc/servers/linux.cfg

# Install Postfix and required software
RUN echo postfix postfix/main_mailer_type string "Internet Site" | debconf-set-selections && \
    echo postfix postfix/mailname string ${NAGIOS_FQDN} | debconf-set-selections && \
    apt-get install -y postfix sasl2-bin mailutils && \
    apt-get clean && rm -Rf /var/lib/apt/lists/* && \
    echo "[smtp.gmail.com]:587 emailaddress@gmail.com:Password" > /etc/postfix/sasl_passwd && \
    postmap hash:/etc/postfix/sasl_passwd && \
    chown root:root /etc/postfix/sasl_passwd /etc/postfix/sasl_passwd.db && \
    chmod 644 /etc/postfix/sasl_passwd /etc/postfix/sasl_passwd.db && \
    echo "/.+/  emailaddress@gmail.com " > /etc/postfix/sender_canonical && \
    postmap hash:/etc/postfix/sender_canonical && \
    chown root:root /etc/postfix/sender_canonical /etc/postfix/sender_canonical.db && \
    chmod 644 /etc/postfix/sender_canonical /etc/postfix/sender_canonical.db && \
    echo "nagios" > /etc/mailname

COPY main.cf /etc/postfix/

ENTRYPOINT service nagios restart && \
           service postfix restart && \
           apachectl -DFOREGROUND
