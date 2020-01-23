FROM prestashop/base:7.2-apache

ENV PS_VERSION 1.7.6.2

# Update log
COPY remoteip.conf /etc/apache2/conf-available/remoteip.conf
RUN a2enmod remoteip && a2enconf remoteip

# Get PrestaShop
ADD https://www.prestashop.com/download/old/prestashop_${PS_VERSION}.zip /tmp/prestashop.zip

# Extract
RUN mkdir -p /tmp/data-ps \
        && unzip -q /tmp/prestashop.zip -d /tmp/data-ps/ \
        && bash /tmp/ps-extractor.sh /tmp/data-ps \
        && rm /tmp/prestashop.zip

