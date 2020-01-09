FROM node:12

# Install Additional Packages
RUN apt-get update \
    && apt-get --yes install \
        rsync \
        curl \
    && rm -rf /var/lib/apt/lists/*

RUN curl -o- -L https://yarnpkg.com/install.sh | bash

RUN mkdir -p /app
WORKDIR /app

EXPOSE 8000
