FROM cbeier/drupal-php:latest

RUN curl -sL https://deb.nodesource.com/setup_7.x | bash - && \
    apt-get update && \
    apt-get install -y \
        nano \
        curl \
        php5-curl \
        nodejs && \
    npm install gulp -g && \
    rm -rf /var/lib/apt/lists/*
