FROM debian:stretch-slim
MAINTAINER Nosto "platforms@nosto.com"
ENV    DEBIAN_FRONTEND noninteractive
# Do not install suggested dependencies
RUN echo -n "APT::Install-Recommends \"false\";\nAPT::Install-Suggests \"false\";" \
      | tee /etc/apt/apt.conf
RUN     test -d /usr/share/man/man1 || mkdir /usr/share/man/man1
# Enable access to metadata and packages using https
RUN     apt-get update && \
      apt-get -y -q install apt-transport-https
# Setup locale
RUN     apt-get update && \
      apt-get -y -q upgrade && \
      apt-get -y -q install apt-utils locales && \
      sed -i 's/^# *\(en_US.UTF-8\)/\1/' /etc/locale.gen && \
      ln -sf /etc/locale.alias /usr/share/locale/locale.alias && \
      locale-gen && \
      apt-get -y -q clean
ENV     LANGUAGE en_US.UTF-8
ENV     LANG en_US.UTF-8
ENV     LC_ALL en_US.UTF-8
ENV     TERM xterm
RUN     groupadd -r plugins -g 113 && \
      useradd -ms /bin/bash -u 113 -r -g plugins plugins && \
      usermod -a -G www-data plugins
# Install all core dependencies required for setting up Apache and PHP atleast
RUN     apt-get -y -q install unzip \
                 wget \
                 libfreetype6-dev \
                 libjpeg-dev \
                 libmcrypt-dev \
                 libreadline-dev \
                 libpng-dev \
                 libicu-dev \
                 default-mysql-client \
                 libmcrypt-dev \
                 libxml2-dev \
                 libxslt1-dev \
                 vim \
                 nano \
                 git \
                 tree \
                 curl \
                 supervisor \
                 build-essential \
                 ca-certificates && \
      apt-get -y clean
RUN     apt-get -y -q install default-jre \
                 default-jdk && \
      apt-get -y clean
# Install Apache, MySQL and all the required development and prod PHP modules
RUN     apt-get -y -q install apache2 \
                 php7.0 \
                 default-mysql-client-core \
                 default-mysql-server-core \
                 default-mysql-server \
                 php7.0-dev \
                 php7.0-gd \
                 php7.0-mcrypt \
                 php7.0-intl \
                 php7.0-xsl \
                 php7.0-zip \
                 php7.0-bcmath \
                 php7.0-curl \
                 php7.0-mbstring \
                 php7.0-mysql \
                 php-ast \
                 php-pear \
                 php7.0-soap && \
      apt-get -y clean
# Upgrade ast extension
RUN     pecl install ast
RUN     wget $(curl https://gist.githubusercontent.com/supercid/41ff58c75440eb82a6f0c4b6fd7bd286/raw/26270a5b2a68f9b4119fef12aafa0d3bbba5d1f6/getPhpStormEAP.php | php)
RUN     tar xfz PhpStorm-*.tar.gz -C /home/plugins/
USER    plugins
#ENTRYPOINT ["bash"]