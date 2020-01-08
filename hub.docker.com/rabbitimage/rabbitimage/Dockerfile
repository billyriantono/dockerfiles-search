FROM ubuntu:17.04
USER root
ENV HOME /root
ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm

# Packages
RUN apt-get update; \
    apt-get -y install \
        software-properties-common \
        python-software-properties \
        language-pack-en-base \
        zip \
        unzip \
        curl \
        wget \
        nano

# Install PHP 7.1
RUN LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php; \
    apt-get update; \
    apt-get -y install \
        php7.1 \
        php7.1-cli \
        php7.1-mcrypt \
        php7.1-dom \
        php7.1-mbstring \
        php7.1-zip \
        php7.1-xml \
        php7.1-intl \
        imagemagick \
        php-imagick \
        librabbitmq4 \
        php-amqp \
        php-uuid \
        php-igbinary

# Admin user
ENV ADMIN_GROUP admin
ENV ADMIN_USER  admin
ENV ADMIN_GID   50000
ENV ADMIN_UID   50000
ENV ADMIN_HOME  /home/${ADMIN_USER}
RUN \
    groupadd -g ${ADMIN_GID} ${ADMIN_GROUP}; \
    useradd -d ${ADMIN_HOME} -s /bin/bash -g ${ADMIN_GROUP} -u ${ADMIN_UID} ${ADMIN_USER}; \
    mkdir ${ADMIN_HOME}; \
    chown ${ADMIN_USER}:${ADMIN_GROUP} ${ADMIN_HOME}; \
    chmod 700 ${ADMIN_HOME}

# Install Composer
ENV COMPOSER_HOME ${ADMIN_DIR}/.composer
RUN mkdir ${COMPOSER_HOME}; \
    chown ${ADMIN_USER}:${ADMIN_GROUP} ${COMPOSER_HOME}; \
    chmod 770 ${COMPOSER_HOME}; \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
ENV PATH ${COMPOSER_HOME}/vendor/bin:$PATH

# Make /app directory
ENV APP_DIR /app
RUN mkdir ${APP_DIR}; \
    chown ${ADMIN_USER}:${ADMIN_GROUP} ${APP_DIR}; \
    chmod 775 ${APP_DIR}

# Build the application
ENV HOME ${ADMIN_HOME}
ENV APP_RESOURCES       ${APP_DIR}/app/resources
ENV APP_EXAMPLES        ${APP_RESOURCES}/examples
ENV APP_DATA_EXAMPLES   ${APP_EXAMPLES}/data
ENV APP_RESULT_EXAMPLES ${APP_EXAMPLES}/result
ENV APP_STORAGE         ${APP_RESOURCES}/storage/data
ENV APP_CSV_STORAGE     ${APP_STORAGE}/csv
ENV APP_JSON_STORAGE    ${APP_STORAGE}/json
ENV APP_YAML_STORAGE    ${APP_STORAGE}/yaml
ENV APP_XML_STORAGE     ${APP_STORAGE}/xml

# Copy source files
COPY ./ ${APP_DIR}/

# Set app permissions
RUN chown -R ${ADMIN_USER}:${ADMIN_GROUP} ${APP_DIR}

# Build app
USER ${ADMIN_USER}
RUN cd ${APP_DIR}; \
    composer dumpautoload; \
    composer update --optimize-autoloader

# Configure the executable
LABEL name="RabbitImage/CLI" description="PHP CLI application to convert images via RabbitMQ"
WORKDIR ${APP_DIR}
ENTRYPOINT ["/bin/bash"]
CMD ["-s"]
USER admin
