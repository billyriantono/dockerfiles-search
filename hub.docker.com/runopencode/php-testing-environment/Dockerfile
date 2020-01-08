FROM php:7.1.1

#####################################################################################
#                                                                                   #
#                                 Setup PHP & Extensions                            #
#                                                                                   #
#####################################################################################

RUN apt-get update && apt-get install -y \
		ca-certificates \
		curl \
		libedit2 \
		libsqlite3-0 \
		libxml2 \
		xz-utils \
		wget \
		zip \
		git \
		autoconf \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libxslt-dev \
        libbz2-dev \
        make \
        unzip \
        wget \
        libicu-dev

RUN docker-php-ext-install bcmath mcrypt zip bz2 mbstring pcntl xsl intl && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install gd && \
    docker-php-ext-install opcache && \
    docker-php-ext-install mbstring pdo pdo_mysql zip


RUN pecl install xdebug-2.5.0 && \
    docker-php-ext-enable xdebug

RUN pecl install apcu && \
    docker-php-ext-enable apcu

RUN echo "memory_limit=-1" > $PHP_INI_DIR/conf.d/memory-limit.ini

RUN echo "date.timezone=${PHP_TIMEZONE:-UTC}" > $PHP_INI_DIR/conf.d/date_timezone.ini

#####################################################################################
#                                                                                   #
#                                 Setup Composer                                    #
#                                                                                   #
#####################################################################################

WORKDIR /tmp

ENV COMPOSER_HOME /composer

# Add global binary directory to PATH and make sure to re-export it
ENV PATH /composer/vendor/bin:$PATH

# Allow Composer to be run as root
ENV COMPOSER_ALLOW_SUPERUSER 1

# Setup the Composer installer
RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
    && curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
    && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }"

RUN php /tmp/composer-setup.php

RUN mv /tmp/composer.phar /usr/local/bin/composer.phar && \
    ln -s /usr/local/bin/composer.phar /usr/local/bin/composer && \
    chmod +x /usr/local/bin/composer


#####################################################################################
#                                                                                   #
# INSTALL JAVA, from https://github.com/frekele/docker-java/blob/jdk8dev/Dockerfile #
#                                                                                   #
#####################################################################################


# Set environment variables for program versions
ENV JDK_VERSION=8
ENV JDK_UPDATE=121
ENV JDK_BUILD=b13
ENV JDK_DISTRO_ARCH=linux-x64
ENV JDK_URL_HASH=e9e7ea248e2c4826b92b3f075a80e441

ENV JCE_FOLDER=UnlimitedJCEPolicyJDK$JDK_VERSION
ENV JDK_FOLDER=jdk1.$JDK_VERSION.0_$JDK_UPDATE
ENV JDK_VERSION_UPDATE=$JDK_VERSION'u'$JDK_UPDATE
ENV JDK_VERSION_UPDATE_BUILD=$JDK_VERSION_UPDATE'-'$JDK_BUILD
ENV JDK_VERSION_UPDATE_DISTRO_ARCH=$JDK_VERSION_UPDATE'-'$JDK_DISTRO_ARCH

ENV JAVA_HOME=/opt/java
ENV JRE_SECURITY_FOLDER=$JAVA_HOME/jre/lib/security
ENV SSL_TRUSTED_CERTS_FOLDER=/opt/ssl/trusted

# Change to tmp folder
WORKDIR /tmp

# Download and extract jdk to opt folder
RUN wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" \
       http://download.oracle.com/otn-pub/java/jdk/${JDK_VERSION_UPDATE_BUILD}/${JDK_URL_HASH}/jdk-${JDK_VERSION_UPDATE_DISTRO_ARCH}.tar.gz \
    && wget --no-check-certificate --no-cookies https://www.oracle.com/webfolder/s/digest/${JDK_VERSION_UPDATE}checksum.html \
    && grep -o "<tr><td>jdk-${JDK_VERSION_UPDATE_DISTRO_ARCH}.tar.gz</td>.*</tr>" ${JDK_VERSION_UPDATE}checksum.html \
        | sed 's/\(<tr>\|<\/tr>\)//g' \
        | sed 's/\(<td>\|<\/td>\)//g' \
        | sed 's/\(<br>\|<\/br>\)//g' \
        | sed "s/\(jdk-${JDK_VERSION_UPDATE_DISTRO_ARCH}.tar.gz\)//g" \
        | awk '{ print $4 }' > jdk-${JDK_VERSION_UPDATE_DISTRO_ARCH}.tar.gz.md5 \
    && echo "$(cat jdk-${JDK_VERSION_UPDATE_DISTRO_ARCH}.tar.gz.md5) jdk-${JDK_VERSION_UPDATE_DISTRO_ARCH}.tar.gz" | md5sum -c \
    && tar -zvxf jdk-${JDK_VERSION_UPDATE_DISTRO_ARCH}.tar.gz -C /opt \
    && ln -s /opt/${JDK_FOLDER} /opt/java \
    && rm -f ${JDK_VERSION_UPDATE}checksum.html \
    && rm -f jdk-${JDK_VERSION_UPDATE_DISTRO_ARCH}.tar.gz \
    && rm -f jdk-${JDK_VERSION_UPDATE_DISTRO_ARCH}.tar.gz.md5

# Download zip file with java cryptography extension and unzip to jre security folder
RUN wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" \
       http://download.oracle.com/otn-pub/java/jce/${JDK_VERSION}/jce_policy-${JDK_VERSION}.zip \
    && unzip jce_policy-${JDK_VERSION}.zip \
    && cp ${JCE_FOLDER}/*.jar ${JRE_SECURITY_FOLDER} \
    && rm -f jce_policy-${JDK_VERSION}.zip \
    && rm -rf ${JCE_FOLDER}

# Add executables to path
RUN update-alternatives --install "/usr/bin/java" "java" "/opt/java/bin/java" 1 && \
    update-alternatives --set "java" "/opt/java/bin/java" && \
    update-alternatives --install "/usr/bin/javac" "javac" "/opt/java/bin/javac" 1 && \
    update-alternatives --set "javac" "/opt/java/bin/javac" && \
    update-alternatives --install "/usr/bin/keytool" "keytool" "/opt/java/bin/keytool" 1 && \
    update-alternatives --set "keytool" "/opt/java/bin/keytool"

# Create trusted ssl certs folder
RUN mkdir -p $SSL_TRUSTED_CERTS_FOLDER

# Mark as volume
VOLUME $SSL_TRUSTED_CERTS_FOLDER

####################################################################################
#                                                                                  #
#                                  INSTALL ANT                                     #
#                                                                                  #
####################################################################################

RUN apt-get install -y ant

####################################################################################
#                                                                                  #
#                               Setup workspace dir                                #
#                                                                                  #
####################################################################################

RUN rm -r /tmp/* && \
    cd / && \
    mkdir /workspace && \
    cd /workspace

WORKDIR /workspace