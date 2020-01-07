FROM jf001z4084/chanco-phpfpm:1.0.6

# -----------------------------------------------------------------------------
# Install SASS and SASS-GLOBBING using Gems
# -----------------------------------------------------------------------------
RUN apt-get update \
&& apt-get install -y libtool automake ruby-full \
&& gem install sass

# -----------------------------------------------------------------------------
# DEFAULT ENVIRONMENT VARIABLES
# -----------------------------------------------------------------------------
ENV CSS_THEME=phoenix \
    APP_ENV='prod' \
    BEANSTALK_HOST='ChancoBeanstalkd' \
    BEANSTALK_PORT='11300' \
    BOWER_INSTALL='true' \
    COMPOSER_INSTALL='true' \
    DATABASE_HOST='chancodb.cipyhhfrgnqn.eu-west-1.rds.amazonaws.com' \
    DATABASE_NAME='chanco' \
    DATABASE_PASS='WiHskY7ZEhpwY4Nf' \
    DATABASE_USER='chanco_admin' \
    DB_INIT='true' \
    ENABLE_XDEBUG='true' \
    ORDER_PREFIX='DE' \
    PHP_INI='dev' \
    REDIS_HOST='ChancoRedis' \
    REDIS_PORT='6379' \
    SITE_NAME='Chanco' \
    ROUTING_PREFIX='' \
    SWATCH_ORDER_EMAIL='' \
    SWATCH_ORDER_EMAIL_FROM='' \
    MAILER_HOST=172.16.19.127 \
    MAILER_PORT=25 \
    MAILER_TRANSPORT='smtp' \
    GA_ANALYTICS='UA-101346448-1' \
    GA_TAGS='GTM-NW2L43S' \
    ENABLE_SECURITY_SERVICE_CHECKOUT='true' \
    ENABLE_SECURITY_SERVICE_SKUBASE='true' \
    AWS_KEY='AKIAJNZYRL24SUV3LY4Q' \
    AWS_SECRETE='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' \
    AWS_IMAGE_BUCKET='upload-images-bucket-v64rleca837do' \
    NEWS_API_KEY='50d7ecca0696444cb292e74122affca6' \
    TEXT_ANALYSIS_API_KEY='3dc5ccf3259dd45e6c6615dab450cfd3' \
    TEXT_ANALYSIS_API_ID='1d8a201c' \
    THUMBNAIL_API='https://tq5rmvnfda.execute-api.eu-west-1.amazonaws.com/thumbnail_generator/'


# -----------------------------------------------------------------------------
# Add Application Code
# -----------------------------------------------------------------------------
#COPY /appcode /var/www/appcode
COPY /appcode /var/www/html

# -----------------------------------------------------------------------------
# Composer install before the cache is invalidated by the new application source files;
# Our dependencies will not be downloaded with every Docker build.
# However, without the source files we cannot run our composer scripts
# or build the autoloader just yet, so we use the --no-scripts and --no-autoloader flags.
# -----------------------------------------------------------------------------





# -----------------------------------------------------------------------------
# Only after we have copied all the source files, we dump the autoloader and run the scripts.
# -----------------------------------------------------------------------------
#RUN composer dump-autoload --optimize \
#    && composer run-script post-install-cmd

# -----------------------------------------------------------------------------
# Install components and compile client.js [Only after we have copied all the source files]
# -----------------------------------------------------------------------------
#RUN cd '/var/www/html' \
#    && bower install --allow-root

# RUN cd '/var/www/html/jssrc' \
#     && npm install \
#     && node_modules/webpack/bin/webpack.js

RUN mkdir -p /var/log/app/monolog \
    && chmod -R 777 /var/log/app

# -----------------------------------------------------------------------------
# COPY CRON
# -----------------------------------------------------------------------------
COPY ./php/crontab/crontab /etc/

# -----------------------------------------------------------------------------
# SETUP CRON AND SUPERVISORD
# -----------------------------------------------------------------------------
COPY ./php/supervisord/supervisord.conf /etc/
COPY ./php/supervisord/conf.d /etc/supervisor/conf.d/
COPY ./php/crontab/crontab /etc/crontab

# -----------------------------------------------------------------------------
# update node and install encore, react
# if yarn run encore dev still not working,
# run following command manually.
# -----------------------------------------------------------------------------

RUN npm cache clean -f \
&&  npm install -g n \
&&  n stable \
&&  npm install --global yarn \
&&  yarn add @symfony/webpack-encore --dev \
&&  yarn add --dev react react-dom prop-types babel-preset-react \
&&  yarn install \
&&  npm install @material-ui/core \
&&  npm install @material-ui/icons
# -----------------------------------------------------------------------------
# Copy Custom Run Command Script
# -----------------------------------------------------------------------------
COPY ./php/run.sh /usr/local/bin/
RUN chmod 755 /usr/local/bin/run.sh
CMD ["/usr/local/bin/run.sh"]

RUN mkdir -p /var/www/html/public/temp \
&&  chmod 777 /var/www/html/public/temp \
&&  cd /var/www/html \
&&  rm -rf vendor/* \
&&  rm -rf composer.lock \
&&  composer upgrade \
&&  composer clearcache \
&&  composer install

VOLUME /var/www/html
VOLUME /var/log
COPY ./error.log /var/log/nginx/error.log
RUN chmod 777 /var/log

EXPOSE 9000