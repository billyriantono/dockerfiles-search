# Installs WordPress with MONEI plugin preinstalled
# Github Repo: https://github.com/MONEI/docker-wordpress-monei

FROM monei/wordpress-monei:4.6.1-php5.6-apache-1.0.0
# Add sudo in order to run wp-cli as the www-data user 
RUN apt-get update && apt-get install -y unzip sqlite3 php5-sqlite && apt-get clean && rm -rf /var/lib/apt/lists/*

COPY rootfs /
RUN curl -o sqlite-plugin.zip https://downloads.wordpress.org/plugin/sqlite-integration.1.8.1.zip && unzip sqlite-plugin.zip -d /opt/
RUN mv /setup-sqlite.sh /bin/setup-sqlite && chmod +x /bin/setup-sqlite && mv /entrypoint.sh /bin/entrypoint && chmod +x /bin/entrypoint

# Cleanup
RUN rm -rf /tmp/* /var/tmp/*

VOLUME /var/lib/wp-database

ENTRYPOINT ["entrypoint"]
CMD ["apache2-foreground"]
