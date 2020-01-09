FROM httpd:2.4

MAINTAINER Jason V jasonmakescoolstuff@gmail.com

# Add in some things
RUN mkdir -p /usr/share/man/man1
# jre install fails because man pages don't have a destination

RUN apt-get update \
        && apt-get install -y \
          nano apt-utils net-tools openssl curl wget procps locate \
          git python \
        && echo "apt-get install nano apt-utils net-tools openssl curl wget procps locate git python" >> /root/install.LOG

#RUN apt-get install -y git python 
#RUN echo "apt-get install -y git python" >> /root/install.LOG

RUN apt-get install gnupg -yq \
        && echo "apt-get install -yq gnupg" >> /root/install.LOG

RUN apt-get install -y -f default-jre \
        && echo "apt-get install -y -f default-jre" >> /root/install.LOG

RUN echo 'alias ll="ls -la --color=auto"' >> /etc/bash.bashrc

RUN echo 'Fix httpd hostname warnings' >> /root/install.LOG

RUN cp /etc/hosts /etc/hosts.new \
        && perl -pi -e "s|`hostname`|`hostname`.shaka.local|g" /etc/hosts.new \
        && echo "Fixing /etc/hosts file" \
        && cat /etc/hosts.new > /etc/hosts \
        && echo "Fixing /etc/hostname file" \
        && echo `hostname`.shaka.local > /etc/hostname \
        && cp /usr/local/apache2/conf/httpd.conf /usr/local/apache2/conf/httpd.conf.OLD \
        && perl -pi -e "s|#ServerName www.example.com:80|ServerName `hostname`.shaka.local:80|g" /usr/local/apache2/conf/httpd.conf \
        && echo "`hostname`.shaka.local" >> /root/install.LOG

RUN echo "*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#" >> /root/install.LOG
# Cobbled a lot of sources together to fix persistent node install failures.
# This helped as well: https://github.com/HabitRPG/habitica/issues/10930

RUN echo "install nodejs using wget and curl" >> /root/install.LOG

RUN wget https://deb.nodesource.com/setup_10.x \
        && chmod +x setup_10.x \
        && ./setup_10.x \
        apt-get update

RUN curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -
RUN echo 'deb https://deb.nodesource.com/node_10.x stretch main' > /etc/apt/sources.list.d/nodesource.list
RUN echo 'deb-src https://deb.nodesource.com/node_10.x stretch main' >> /etc/apt/sources.list.d/nodesource.list

RUN apt-get update; apt-get install -y nodejs
#RUN apt-get install -y nodejs

RUN echo "NODE PART DONE" >> /root/install.LOG

RUN echo "*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#*#" >> /root/install.LOG

#*********************************SHAKA**PLAYER***********************
# Shaka part. Note that this installs latest.
RUN echo "Install latest shaka-player" >> /root/install.LOG
RUN git clone https://github.com/google/shaka-player.git \
  && echo "Git pull"  >> /root/install.LOG

WORKDIR shaka-player

RUN python build/all.py \
  && echo "python build/all.py" >> /root/install.LOG

# Make shaka-player demo accessible via browser
RUN echo "Make shaka-player demo accessible via browser" >> /root/install.LOG
RUN chgrp -R www-data ../shaka-player
RUN cp -r ../shaka-player /usr/local/apache2/htdocs/.
WORKDIR /root
RUN rm -rf ../shaka-player
#**************************END****SHAKA**PLAYER***********************



#*******************************CERTS*********************************
# Generate Self-Signed Certs
RUN echo "SSL Self-signed Certs"  >> /root/install.LOG

RUN openssl req -new -x509 -newkey rsa:2048 -nodes \
        -out /usr/local/apache2/conf/server.crt -days 365 \
        -keyout /usr/local/apache2/conf/server.key \
        -subj "/C=US/ST=WA/L=Seattle/O=IT/OU=SHAKA/CN=shaka.local"

# Customize httpd.conf to use your certs
RUN echo "Customize httpd.conf to pick up ssl certs" >> /root/install.LOG

RUN sed -i \
        -e 's/^#\(Include .*httpd-ssl.conf\)/\1/' \
        -e 's/^#\(LoadModule .*mod_ssl.so\)/\1/' \
        -e 's/^#\(LoadModule .*mod_socache_shmcb.so\)/\1/' \
        /usr/local/apache2/conf/httpd.conf

RUN perl -pi -e "s|VirtualHost _default_:443|VirtualHost *:443|g" /usr/local/apache2/conf/extra/httpd-ssl.conf \
        && perl -pi -e "s|ServerName www.example.com:443|ServerName `hostname`.shaka.local:443|g" /usr/local/apache2/conf/extra/httpd-ssl.conf \
        && echo `hostname`.shaka.local > /etc/hostname \
        && perl -pi -e 's|#SSLCertificateChainFile "/usr/local/apache2/conf/server-ca.crt"|SSLCertificateChainFile "/usr/local/apache2/conf/server.crt"|g' /usr/local/apache2/conf/extra/httpd-ssl.conf \
        && apachectl restart

#*************************END***CERTS*********************************

#EXPOSE web port for player UI
EXPOSE 443/tcp

#*******************************CONTENT*******************************
#                        PLACING ALL IN WEBROOT
WORKDIR /usr/local/apache2/htdocs/
RUN echo "Copy and untar content"  >> /root/install.LOG

COPY llama.tgz .
RUN tar -xzf llama.tgz

#*************************Shaka Demo Config**************************
#                Setting content and license server IPs
RUN echo "*************************Shaka Demo Config**************************"  >> /root/install.LOG
RUN echo "Customize the shaka config to pick up IPs and content" >> /root/install.LOG

# moving to a one-way-door script for first-login.

# Boilerplate
COPY assets.js /usr/local/apache2/htdocs/shaka-player/demo/common/.

#TODO The below references are not right. Local is the docker internal IP.
# Scripts to get unique server data
COPY *.sh /usr/local/apache2/htdocs/shaka-player/demo/common/
#COPY getmylocalip.sh /usr/local/apache2/htdocs/shaka-player/demo/common/.

# Scripts to set config with server data
#COPY fixAssetsJs.sh /usr/local/apache2/htdocs/shaka-player/demo/common/.
COPY fixAssetsJsHelper.py /usr/local/apache2/htdocs/shaka-player/demo/common/.

#COPY one-way-door.sh /usr/local/apache2/htdocs/shaka-player/demo/common/.
RUN chmod +x /usr/local/apache2/htdocs/shaka-player/demo/common/*.sh

ENV MACHINE_IP="0.0.0.0"
# Get unique server data
# Moved all IP setting config stuff to a one-way-door script.

#************************DEBUGGING STUFF*******************************
RUN updatedb

RUN echo "Use https://proxy.uat.widevine.com/proxy for your" >> /root/install.LOG
RUN echo "license server if you are not running one locally!" >> /root/install.LOG

RUN echo "Install complete." >> /root/install.LOG

RUN echo "First login runs /usr/local/apache2/htdocs/shaka-player/demo/common/one-way-door.sh" >> /root/install.LOG

CMD ["/bin/bash", "/usr/local/apache2/htdocs/shaka-player/demo/common/one-way-door.sh"]

#************************END****INSTALL*******************************

#*********************************TESTS*******************************
# Add things for test frameworks (Not working headless yet)
# Chrome
#RUN mkdir chrome
#WORKDIR chrome

#RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - 
#RUN sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
#RUN apt-get update
#RUN apt-get install -y google-chrome-stable

# Headless
#RUN apt-get install -y xvfb

# Firefox
# RUN apt-get install -y firefox-esr
#**************************END****TESTS*******************************
