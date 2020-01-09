FROM neuseelandhaus/devops-php:7.0

# fetch application
RUN apt-get update && apt-get install -y tar rsync sudo less mysql-client

RUN curl -o /usr/local/bin/wp https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
&&  chmod +x /usr/local/bin/wp

WORKDIR /app_git
ADD . /app_git

WORKDIR /temp

RUN curl -o ./_wp.tar.gz --location https://github.com/WordPress/WordPress/archive/$(cat /app_git/WP_VERSION).tar.gz \
    && mkdir ./wordpress \
    && tar -xzf _wp.tar.gz -C ./wordpress \
    && mkdir /app \
    && mv ./wordpress/WordPress-$(cat /app_git/WP_VERSION)/* /app \
    && rm ./_wp.tar.gz

WORKDIR /

RUN rsync -a -v /app_git/ /app/ \
    && rm -rf /app_git \
    && rm -rf /app/.git \
    && chown -R www-data /app \
    && rm -rf /root/.ssh

RUN apt-get remove -y rsync libxml++2.6-dev apt-utils libmcrypt-dev libicu-dev libxslt-dev libpng12-dev libjpeg62-turbo-dev libfreetype6-dev \
    && apt-get autoremove -y
#end fetch application


VOLUME /app

WORKDIR /

CMD ["/bin/echo", "-n"]
