FROM gekvansoftware/php:7.2

# File Author / Maintainer
MAINTAINER Marc-Jan Barnhoorn

ENV COMPOSER_HOME /composer

# Set up the application directory
VOLUME ["/app"]
WORKDIR /app

COPY docker-entrypoint.sh /

# Set up the command arguments
CMD ["-"]
ENTRYPOINT ["/docker-entrypoint.sh"]
