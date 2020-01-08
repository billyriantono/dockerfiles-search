FROM willhallonline/composer:alpine

RUN cd /usr/lib \
    && mkdir drush \
    && cd drush \
    && composer require drush/drush \
    && ln -s /usr/lib/drush/vendor/bin/drush /usr/local/bin/drush

RUN cd /usr/lib/ \
    && mkdir drush8 \
    && cd drush8 \
    && composer require drush/drush:8.x \
    && ln -s /usr/lib/drush8/vendor/bin/drush /usr/local/bin/drush8
