FROM nextcloud:14

# Copy in some modified versions of the Apache configs from the default
# container. Nothing has been changed here except modifying the port
# that Apache listens on from :80 to :8080 so we can run it without root.
COPY ports.conf /etc/apache2/ports.conf
COPY 000-default.conf /etc/apache2/sites-enabled/000-default.conf

USER www-data

# We don't need to specify an entrypoint here, as it'll use the one
# already set in the Nextcloud image.
