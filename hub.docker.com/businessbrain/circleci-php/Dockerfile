FROM circleci/php:latest

WORKDIR /home/circleci

# Install PHP_CodeSniffer & PHP Compatibility
RUN composer global require "squizlabs/php_codesniffer=*" && \
    composer global require "phpcompatibility/php-compatibility=*"

# Set PATH
ENV PATH="${PATH}:/home/circleci/.composer/vendor/bin"

# Set WordPress Coding Standards
RUN git clone -b master https://github.com/WordPress-Coding-Standards/WordPress-Coding-Standards.git ~/.composer/vendor/squizlabs/php_codesniffer/CodeSniffer/Standards && \
    phpcs --config-set installed_paths /home/circleci/.composer/vendor/squizlabs/php_codesniffer/CodeSniffer/Standards
