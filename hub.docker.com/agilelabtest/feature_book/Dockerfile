FROM agilelabtest/alpine-nodejs

WORKDIR /app

# Install bash
RUN apk add --no-cache bash gawk sed grep bc coreutils

# Install jq
RUN apk --update add jq && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*

# Install git
RUN apk --update add git openssh && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*

# Install FeatureBook
RUN npm install -g featurebook
COPY get_feature_book.sh /usr/bin/get_feature_book
RUN chmod +x /usr/bin/get_feature_book

WORKDIR /src
