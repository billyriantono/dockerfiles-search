FROM nerelohw/docker-php7

# Actualize confih.php.tpl when updating version.
ENV WEBGRIND_VER="1.5" \
    WEBGRIND_PROJECT=/root/webgrind \
    WEBGRIND_VENDOR=/root/webgrind/vendor/jokkedk/webgrind

RUN apk add --update --no-cache graphviz python3 && \
    ln -s /usr/bin/python3 /usr/bin/python && \
    apk add --update --no-cache --virtual build-deps g++ make && \
    mkdir ${WEBGRIND_PROJECT} && cd ${WEBGRIND_PROJECT} && composer require jokkedk/webgrind:^${WEBGRIND_VER} && \
    cd "${WEBGRIND_VENDOR}" && \
    sed -i "s/Europe\/Copenhagen/America\/New_York/g" ${WEBGRIND_VENDOR}/config.php && \
    make && \
    apk del build-deps && \
    composer clear-cache 

WORKDIR "${WEBGRIND_VENDOR}"

EXPOSE 80

VOLUME ["/tmp"]

CMD ["php", "-S", "0.0.0.0:80", "index.php"]
