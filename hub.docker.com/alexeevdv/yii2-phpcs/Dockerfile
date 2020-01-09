FROM willhallonline/composer

# Install PHPCS
RUN composer global require "squizlabs/php_codesniffer" "^3.0" \
    # Retrieve Yii2 Coding Standards
    && composer global require "yiisoft/yii2-coding-standards" "^2.0" \
    # Set Yii2 as default CodeSniffer Standard
    && phpcs --config-set installed_paths /root/.composer/vendor/yiisoft/yii2-coding-standards \
    && phpcs --config-set default_standard Yii2

WORKDIR /app

CMD ["phpcs"]
CMD ["phpcbf"]
