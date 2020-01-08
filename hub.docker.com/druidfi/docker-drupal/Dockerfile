FROM amazeeio/drupal:php71-basic

RUN rm /etc/apt/sources.list.d/mycli.list && \
    #
    # Update Yarn key
    #
    wget -q -O yarnpkg.gpg.pub https://dl.yarnpkg.com/debian/pubkey.gpg && \
    gpg yarnpkg.gpg.pub && \
    apt-key add yarnpkg.gpg.pub && \
    #
    # Update Blackfire key
    #
    wget -q -O blackfire.gpg.pub https://packages.blackfire.io/gpg.key && \
    gpg blackfire.gpg.pub && \
    apt-key add blackfire.gpg.pub && \
    #
    # Update packages
    #
    apt-get update && \
    apt-get -y --no-install-recommends install unzip && \
    #
    # Update Composer
    #
    composer self-update && \
    #
    # Add hirak/prestissimo Composer plugin
    #
    composer global require --optimize-autoloader "hirak/prestissimo" && \
    composer global dumpautoload --optimize && \
    #
    # Cleanup
    #
    composer clear-cache && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/www/drupal/public_html/*.gpg.pub
