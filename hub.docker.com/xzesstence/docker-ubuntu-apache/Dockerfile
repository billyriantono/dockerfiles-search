FROM xzesstence/docker-ubuntu

RUN \
apt-get update && \
apt-get install -y apache2 wget curl


RUN \
apt-get install -y php7.0 libapache2-mod-php7.0 php7.0-cli && apt-get install -y -q php7.0-gd php7.0-intl php7.0-xml php7.0-mysql php7.0-mcrypt php7.0-zip

RUN service apache2 restart
