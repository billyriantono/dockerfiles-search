FROM composer:latest

# https://github.com/hirak/prestissimo
# ... downloads packages in parallel to speed up the installation process.
RUN composer global require hirak/prestissimo

# add privileges to run container as a non root user
RUN chmod -R 777 /tmp