FROM php:7.2.26-alpine3.9

RUN apk --update --no-cache add libzip-dev \
    libxml2-dev \ 
    zlib-dev \
    bash \
    curl \
    jq \
    openssl \ 
    ca-certificates

# Add GIT
RUN apk add --no-cache git

# Install PHP modules
RUN docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install simplexml \
    && docker-php-ext-install xml \
    && docker-php-ext-install tokenizer \
    && docker-php-ext-install fileinfo \
    && docker-php-ext-install soap
RUN docker-php-ext-configure zip \
    && docker-php-ext-install zip

# Add Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Add Python PIP + AWS CLI
RUN apk -v --update add \
    python \
    py-pip \
    && \
    pip install --upgrade awscli && \
    rm /var/cache/apk/*

# Add RSync
RUN apk add rsync

# Add HELM
RUN curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 > get_helm.sh && \
    chmod u+x get_helm.sh && \
    ./get_helm.sh

# Avoid Gitlab permission issue
RUN mkdir -p /etc/deploy

# Add NodeJs + NPM
RUN apk add --update nodejs npm

# Add Kubectl
# Note: Latest version may be found on:
# https://aur.archlinux.org/packages/kubectl-bin/
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl && \
    chmod +x ./kubectl && \
    mv ./kubectl /usr/local/bin/kubectl
