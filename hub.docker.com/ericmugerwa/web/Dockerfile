FROM ericmugerwa/apache-php:2.4-7.1

USER root

# Make storage directory
RUN echo "Making storage directory"; \
    cd ${APP_DIR}; \
    mkdir -p storage/app; \
    mkdir -p storage/logs; \
    mkdir -p storage/framework/cache; \
    mkdir -p storage/framework/sessions; \
    mkdir -p storage/framework/testing; \
    mkdir -p storage/framework/views; \
    chown -R ${ADMIN_USER}:${APACHE_GROUP} storage; \
    chmod -R 775 storage

# Install composer deps: vendor/
USER ${ADMIN_USER}
COPY artisan ${APP_DIR}/
COPY app ${APP_DIR}/app
COPY bootstrap ${APP_DIR}/bootstrap
COPY config ${APP_DIR}/config
COPY routes ${APP_DIR}/routes
COPY database ${APP_DIR}/database
COPY tests ${APP_DIR}/test
COPY composer.json ${APP_DIR}/
COPY composer.lock ${APP_DIR}/
USER root
RUN echo "Preparing to install Composer deps in ${APP_DIR}/vendor"; \
    cd ${APP_DIR}; \
    mkdir vendor; \
    chown -R ${ADMIN_USER}:${APACHE_GROUP} vendor; \
    chmod 775 vendor; \
    chown ${ADMIN_USER}:${ADMIN_GROUP} composer.json; \
    chown ${ADMIN_USER}:${ADMIN_GROUP} composer.lock; \
    chown -R ${ADMIN_USER}:${APACHE_GROUP} bootstrap/cache; \
    chmod 775 bootstrap/cache

# Composer install
USER ${ADMIN_USER}
RUN echo "Installing Composer deps in ${APP_DIR}/vendor"; \
    cd ${APP_DIR}; \
    composer dumpautoload; \
    composer install

# Install node deps: node_modules/
USER root
USER ${ADMIN_USER}
COPY package.json ${APP_DIR}/
RUN cd ${APP_DIR}; \
    npm cache clear; \
    npm install --no-optional

# Install Bower deps: resources/bower_components/
USER root
COPY bower.json ${APP_DIR}/
COPY .bowerrc ${APP_DIR}/
COPY resources/ ${APP_DIR}/resources
ENV BOWER_DIR ${APP_DIR}/resources/assets/bower
RUN echo "Making Bower directory: ${BOWER_DIR}"; \
    mkdir ${BOWER_DIR}; \
    chown ${ADMIN_USER}:${APACHE_GROUP} ${BOWER_DIR}; \
    chmod 755 ${BOWER_DIR}
USER ${ADMIN_USER}
RUN echo "Installing Bower resources in ${BOWER_DIR}"; \
    cd ${APP_DIR}; \
    bower install

# Gulp
USER root
RUN cd ${APP_DIR}; \
    mkdir public
COPY public/ ${APP_DIR}/public/
RUN cd ${APP_DIR}; \
    chown -R ${ADMIN_USER}:${APACHE_GROUP} public; \
    chmod 755 public
COPY gulpfile.js ${APP_DIR}/
USER ${ADMIN_USER}
RUN echo "Running Gulp tasks"; \
    cd ${APP_DIR}; \
    gulp

# Server config files
USER root
COPY config/docker/apache/apache2.conf          /etc/apache2/
COPY config/docker/apache/app.conf              /etc/apache2/sites-available/
COPY config/docker/apache/ports.conf            /etc/apache2/
COPY config/docker/php/10-app.ini               ${PHP_APACHE_INI}
COPY config/docker/php/10-app.ini               ${PHP_CLI_INI}
COPY config/docker/supervisord/supervisord.conf /etc/supervisor/conf.d/

# App config files
COPY .env.example ${APP_DIR}/.env

# Configure the executable
USER root
LABEL name="EricMugerwa/Web-Deps" description="Web application"
WORKDIR ${APP_DIR}
COPY config/docker/entrypoint.sh /entrypoint.sh
RUN chown ${ADMIN_USER}:${ADMIN_GROUP} /entrypoint.sh; \
    chmod 500 /entrypoint.sh; \
    chmod +x /entrypoint.sh
ENTRYPOINT ["/bin/bash"]
CMD ["/entrypoint.sh"]
