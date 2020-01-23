FROM alledia/composer

MAINTAINER Alledia <suport@alledia.com>

# Install Codeception
ADD codecept.phar /opt/codecept.phar
RUN ln -s /opt/codecept.phar /usr/bin/codecept \
    && chmod +x /usr/bin/codecept

