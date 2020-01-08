FROM nimmis/apache-php5

RUN apt-get update && apt-get update -y
RUN apt-get install -y php-pear php5-dev php5-xdebug

# Setting xdebug 
RUN echo "error_reporting = E_ALL" >> /etc/php5/apache2/conf.d/20-xdebug.ini \
    && echo "display_startup_errors = On" >> /etc/php5/apache2/conf.d/20-xdebug.ini \
    && echo "display_errors = On" >> /etc/php5/apache2/conf.d/20-xdebug.ini \
    && echo "xdebug.remote_enable=1" >> /etc/php5/apache2/conf.d/20-xdebug.ini \
    && echo "xdebug.remote_connect_back=1" >> /etc/php5/apache2/conf.d/20-xdebug.ini \
    && echo "xdebug.remote_autostart=1" >> /etc/php5/apache2/conf.d/20-xdebug.ini \
    && echo "xdebug.idekey=PHPSTORM" >> /etc/php5/apache2/conf.d/20-xdebug.ini \
    && echo "xdebug.remote_port=9000" >> /etc/php5/apache2/conf.d/20-xdebug.ini \
    && echo "xdebug.remote_handler=dbgp" >> /etc/php5/apache2/conf.d/20-xdebug.ini \
    && echo "xdebug.max_nesting_level=500" >> /etc/php5/apache2/conf.d/20-xdebug.ini \
    && echo "xdebug.remote_host=10.0.75.1" >> /etc/php5/apache2/conf.d/20-xdebug.ini

# Creating Aliases
RUN echo 'alias ll="ls -alF"' >> /etc/bash.bashrc && \
    echo 'alias la="ls -A"' >> /etc/bash.bashrc && \
    echo 'alias l="ls -CF"' >> /etc/bash.bashrc

# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /var/www

EXPOSE 80

# Define default command.
CMD ["/my_init"]