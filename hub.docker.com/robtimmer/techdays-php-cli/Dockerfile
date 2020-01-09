# Extend from PHP CLI Alpine image
FROM php:cli-alpine3.7

# Set maintainer information
MAINTAINER rob@robtimmer.com

# Install bash and VIM
RUN apk --no-cache --update add bash vim

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Set entrypoint to bash
ENTRYPOINT ["/bin/bash"]
