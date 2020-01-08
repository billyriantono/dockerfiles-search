FROM php:7.1.1-alpine

LABEL authors="AndyMardell, herloct"

ENV PHPCS_VERSION=3.3.2
ENV WPCS_VERSION=2.1.1

RUN curl -L https://github.com/squizlabs/PHP_CodeSniffer/releases/download/$PHPCS_VERSION/phpcs.phar > /usr/local/bin/phpcs && \
    curl -L https://github.com/squizlabs/PHP_CodeSniffer/releases/download/$PHPCS_VERSION/phpcbf.phar > /usr/local/bin/phpcbf && \
    chmod +x /usr/local/bin/phpcbf && \
    chmod +x /usr/local/bin/phpcs && \
    apk update && apk upgrade && \
    apk add git && \
    git clone -b master https://github.com/WordPress/WordPress-Coding-Standards.git /wpcs && \
    cd /wpcs && git checkout tags/$WPCS_VERSION && \
    rm -rf /var/cache/apk/* /var/tmp/* /tmp/* && \
    phpcs --config-set installed_paths /wpcs && \
    phpcs --config-set colors 1 && \
    phpcs --config-set show_progress 1 && \
    phpcs --config-set report_width 200

VOLUME ["/project"]
WORKDIR /project

ENTRYPOINT ["phpcs"]
CMD ["--version"]
