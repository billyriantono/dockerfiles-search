FROM avnir/composer:latest
MAINTAINER Avni Rexhepi <arexhepi@gmail.com>


RUN apt-get update && apt-get install -y \
            mysql-client-5.6 nodejs npm \
            --no-install-recommends && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


RUN ln -s `which nodejs` /usr/bin/node


RUN npm install -g gulp && \
    npm install -g bower && \
    npm install -g grunt-cli


RUN echo "{ \"allow_root\":  true, \"interactive\": false }" >> /.bowerrc
RUN composer global require "phpunit/phpunit=4.8.*" && \
    echo "export PATH=~/.composer/vendor/bin/:$PATH" >> ~/.bashrc && \
    ln -s ~/.composer/vendor/bin/phpunit /usr/local/bin/phpunit && \
    rm -Rf /var/www/*


ENTRYPOINT ["/bin/sh", "-c"]
CMD ["phpunit"]