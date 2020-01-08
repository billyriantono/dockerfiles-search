FROM composer
RUN apk --update add jq rsync openssh && rm -rf /var/lib/apt/lists/* && rm /var/cache/apk/*
RUN composer global require pantheon-systems/terminus:2.0.1
ENV PATH="/tmp/vendor/bin:${PATH}"
