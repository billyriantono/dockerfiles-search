FROM ubuntu:latest
RUN apt-get update && apt-get install -y --no-install-recommends mysql-client curl software-properties-common wget git nano varnish && apt-add-repository -y ppa:nginx/stable && \
    apt-add-repository ppa:ondrej/php && apt-get install -y --no-install-recommends nginx && \
    DEBIAN_FRONTEND=noninteractive apt-get -y --no-install-recommends install php7.1-fpm php7.1-cli php7.1-common php7.1-gd \
    php7.1-mysql php7.1-mcrypt php7.1-curl php7.1-intl php7.1-xsl \
    php7.1-mbstring php7.1-zip php7.1-bcmath php7.1-iconv php7.1-imap \ 
    php7.1-xmlrpc php7.1-dev php7.1-soap && apt-get -y autoremove && apt-get -y autoclean && \
    rm -rf /var/lib/apt/lists/* && git clone https://github.com/WordPress/WordPress.git /var/www/wordpress

# Copy nginx config
COPY config/wordpress.conf /etc/nginx/sites-available/
RUN ln -s /etc/nginx/sites-available/wordpress.conf /etc/nginx/sites-enabled/wordpress.conf
RUN rm -rf /etc/nginx/sites-enabled/default
WORKDIR /var/www/wordpress/

# Setup entrypoint
EXPOSE 80
COPY start.sh /
RUN chmod +x /start.sh && chown root:root /start.sh
ENTRYPOINT /start.sh