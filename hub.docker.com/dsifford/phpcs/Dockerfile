FROM alpine:3.10 as builder
ARG phpcs_version=
ARG wpcs_version=master

RUN apk add --no-cache \
    grep \
    curl \
    tar

WORKDIR /build

RUN mkdir -p wpcs/Custom && \
    curl -L "https://github.com/WordPress-Coding-Standards/WordPress-Coding-Standards/tarball/$wpcs_version" | tar xz -C wpcs --strip-components 1 && \
    curl \
        -OL "https://github.com/squizlabs/PHP_CodeSniffer/releases/download/${phpcs_version:-$(curl -s https://api.github.com/repos/squizlabs/PHP_CodeSniffer/releases/latest | grep -oP '"tag_name": "\K(.*)(?=")')}/phpcs.phar" \
        -OL "https://github.com/squizlabs/PHP_CodeSniffer/releases/download/${phpcs_version:-$(curl -s https://api.github.com/repos/squizlabs/PHP_CodeSniffer/releases/latest | grep -oP '"tag_name": "\K(.*)(?=")')}/phpcbf.phar"

COPY ruleset.xml wpcs/Custom/ruleset.xml

FROM php:7-cli
LABEL maintainer="dereksifford@gmail.com"

WORKDIR /root

COPY --from=builder /build .

RUN php phpcs.phar --config-set installed_paths /root/wpcs && \
    php phpcs.phar --config-set default_standard Custom

WORKDIR /app
ENTRYPOINT ["php", "/root/phpcs.phar"]
