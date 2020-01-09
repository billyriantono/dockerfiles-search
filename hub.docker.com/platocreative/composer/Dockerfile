FROM composer:latest

# Installs a parallel processing plugin to improve composer performance,
# then we run composer install. We can probably remove this into a build container in the future.
RUN composer global require hirak/prestissimo