FROM joaquindlz/rpi-docker-lamp:latest
COPY qemu-arm /usr/bin/qemu-arm

ENV DEBIAN_FRONTEND noninteractive

# this forces dpkg not to call sync() after package extraction and speeds up install
RUN echo "force-unsafe-io" > /etc/dpkg/dpkg.cfg.d/02apt-speedup
# we don't need and apt cache in a container
RUN echo "Acquire::http {No-Cache=True;};" > /etc/apt/apt.conf.d/no-cache

# Initialize application
WORKDIR /app

# Install composer && global asset plugin (Yii 2.0 requirement)
ENV COMPOSER_HOME /root/.composer
ENV PATH /root/.composer/vendor/bin:$PATH
ADD config.json /root/.composer/config.json
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    /usr/local/bin/composer global require "fxp/composer-asset-plugin"

# Install application template and packages
# Yii 2.0 application and its extensions can be used directly from the image or serve as local cache
RUN /usr/local/bin/composer create-project --prefer-dist \
    yiisoft/yii2-app-basic:2.* \
    /app
	
ADD run.sh /root/run.sh
RUN chmod 700 /root/run.sh
CMD ["/root/run.sh"]

EXPOSE 80 
