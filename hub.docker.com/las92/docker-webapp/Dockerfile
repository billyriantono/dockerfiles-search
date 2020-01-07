FROM webdevops/php-apache:debian-8

ENV TZ=Europe/Paris
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone


#RUN apt-get update && apt-get install -y xvfb wkhtmltopdf
RUN apt-get update && apt-get install -y build-essential
RUN curl -sL https://deb.nodesource.com/setup_7.x | bash -
RUN apt-get install -y nodejs
RUN npm install bower -g
RUN npm install gulp -g

RUN curl -sSL https://getcomposer.org/installer | \
    php -- --install-dir=/usr/local/bin --filename=composer


