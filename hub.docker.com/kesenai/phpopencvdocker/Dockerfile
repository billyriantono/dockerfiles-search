FROM debian:9

RUN apt update \
    && apt install -y pkg-config cmake git php-cli php-dev wget gnupg curl git zip

RUN git clone https://github.com/opencv/opencv_contrib.git \
    && git clone https://github.com/opencv/opencv.git

RUN cd opencv_contrib \
    && git checkout tags/4.0.1 \
    && cd ../opencv \
    && git checkout tags/4.0.1 \
    && cd .. \
    && mkdir build \
    && cd build \
    && cmake -D OPENCV_GENERATE_PKGCONFIG=YES -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D OPENCV_EXTRA_MODULES_PATH=../opencv_contrib/modules ../opencv \
    && make -j4 \
    && make install \
    && ldconfig \
    && cd ../..

RUN git clone https://github.com/php-opencv/php-opencv.git \
    && cd php-opencv \
    && phpize \
    && ./configure --with-php-config=/usr/bin/php-config \
    && make \
    && make install \
    && echo "extension=opencv.so" > /etc/php/7.0/cli/conf.d/opencv.ini

RUN cd / \
    && rm -rf opencv \
    && rm -rf opencv_contrib \
    && rm -rf php-opencv

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /tmp
ENV COMPOSER_VERSION 1.8.4

RUN curl --silent --fail --location --retry 3 --output /tmp/installer.php --url https://raw.githubusercontent.com/composer/getcomposer.org/cb19f2aa3aeaa2006c0cd69a7ef011eb31463067/web/installer \
 && php -r " \
    \$signature = '48e3236262b34d30969dca3c37281b3b4bbe3221bda826ac6a9a62d6444cdb0dcd0615698a5cbe587c3f0fe57a54d8f5'; \
    \$hash = hash('sha384', file_get_contents('/tmp/installer.php')); \
    if (!hash_equals(\$signature, \$hash)) { \
        unlink('/tmp/installer.php'); \
        echo 'Integrity check failed, installer is either corrupt or worse.' . PHP_EOL; \
        exit(1); \
    }" \
 && php /tmp/installer.php --no-ansi --install-dir=/usr/bin --filename=composer --version=${COMPOSER_VERSION} \
 && composer --ansi --version --no-interaction \
 && rm -f /tmp/installer.php