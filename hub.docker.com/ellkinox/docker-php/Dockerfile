FROM ellkinox/docker-debian:8-slim

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -qq

RUN apt-get -y -f install libapache2-mod-fcgid php-pear webalizer apache2-suexec-custom

# Install php7.2
RUN apt-get -y -f install php7.2 php7.2-cli php7.2-mbstring php7.2-xml php7.2-odbc php7.2-common libapache2-mod-php7.2 \
                php7.2-gd php7.2-fpm php7.2-imap php7.2-curl php7.2-mb php7.2-opcache php7.2-mysql php7.2-json \
                php7.2-intl php7.2-zip php7.2-readline

CMD ["bash"]