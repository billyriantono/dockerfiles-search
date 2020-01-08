FROM ubuntu:18.04

RUN apt-get update -y && apt-get install -y gnupg
RUN echo "deb http://ppa.launchpad.net/ansible/ansible-2.5/ubuntu bionic main" > /etc/apt/sources.list.d/ansible.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
RUN echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu bionic main" > /etc/apt/sources.list.d/php.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 4F4EA0AAE5267A6C

RUN apt-get update -y && \
            DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
            ansible \
            locales \
            curl \
            rsync \
            apache2 \
            libapache2-mod-php7.2 \
            php7.2-bz2 php7.2-cgi php7.2-cli php7.2-common \
            php7.2-curl php7.2-gd php7.2-intl php7.2-json php7.2-mbstring php7.2-mysql php7.2-opcache \
            php7.2-readline php7.2-soap php7.2-xml php7.2-xmlrpc php7.2-xsl php7.2-zip php-xcache \
            && \
            apt-get clean

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

ENV TZ=Asia/Phnom_Penh
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN a2enmod actions alias expires headers rewrite ssl
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

COPY conf/apache/envvars /etc/apache2/envvars
WORKDIR /var/www/html

COPY conf/scripts/entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]

EXPOSE 80
EXPOSE 443
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
