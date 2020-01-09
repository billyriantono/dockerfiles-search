FROM wordpress

# Copy theme
COPY ./wordpress/wp-content/themes/uslandingpage/ /var/www/html/wp-content/themes/uslandingpage/

# Copy language
COPY ./wordpress/wp-content/languages/ /var/www/html/wp-content/languages/

# Copy plugin
COPY ./wordpress/wp-content/plugins/ /var/www/html/wp-content/plugins/

# Copy Upload
COPY ./wordpress/wp-content/uploads/ /var/www/html/wp-content/uploads/

# Copy launcher
COPY launcher.sh /usr/src/app/usgroup/

# launcher
RUN ["chmod", "+x", "/usr/src/app/usgroup/launcher.sh"]
ENTRYPOINT [ "/usr/src/app/usgroup/launcher.sh" ]