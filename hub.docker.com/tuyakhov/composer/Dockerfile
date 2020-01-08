#########################################################################
#
# Composer container - used by our PHP applications
#
# Build with:
#  docker build -t="tuyakhov/composer" .
#
#
########################################################################

FROM tuyakhov/stombox-php

# Install composer itself
RUN apt-get install -y curl git subversion mercurial
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN composer self-update

# Add access token to get enough API rate-limit to retrieve the dependent package information from Github
RUN composer config -g github-oauth.github.com ea4daec301f36fb9405555eb84db19392678aa52

# Install composer asset plugin
RUN composer global require "fxp/composer-asset-plugin:~1.0"

# Make composer the default command
ENTRYPOINT ["composer", "--ansi", "--no-interaction"]

VOLUME ["/code"]

WORKDIR /code
