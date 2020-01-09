# This builds a LDAP Account Manager Docker container

FROM ubuntu:14.04
MAINTAINER Fabian Gut <fabian.gut@inftec.ch>, InfTec GmbH

# These values can and should be configured
ENV LAM_VERSION 4.9

# Install Curl
RUN apt-get update && \
    apt-get install -y \
        apache2 \
        curl \
        php5 \
        php5-ldap && \
    apt-get autoclean
        
# Install LAM
RUN curl -Lks http://downloads.sourceforge.net/sourceforge/lam/ldap-account-manager-${LAM_VERSION}.tar.bz2 -o /root/lam.tar.bz2
RUN rm /var/www/html/index.html && tar xjf /root/lam.tar.bz2 --strip=1 -C /var/www/html && rm /root/lam.tar.bz2
RUN cp -r /var/www/html/config /var/www/html/config.old

# Copy assets
COPY assets/lam.init /opt/lam-setup/lam.init
COPY assets/scripts/config_cron.sh /opt/lam-scripts/config_cron.sh
COPY assets/scripts/crontab /etc/cron.d/config-cron
RUN chmod 755 /opt/lam-setup/lam.init
RUN chmod 755 /opt/lam-scripts/config_cron.sh
RUN chmod 644 /etc/cron.d/config-cron

VOLUME /opt/lam-config
EXPOSE 80
ENTRYPOINT ["/opt/lam-setup/lam.init"]
CMD ["lam:start"]

