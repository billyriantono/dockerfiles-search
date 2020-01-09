# Introduction
FROM redis:alpine
LABEL maintainer="maximetavernier92@gmail.com"
LABEL version="0.0.2"

# Install dependencies
RUN apk add --update --no-cache zip perl openssl nodejs && \
    rm -rf /var/cache/apk/*

# Create archi
RUN mkdir -p /app
WORKDIR /app
COPY . /app

# Install dependencies
RUN npm install -g jsawk typescript npx --silent
RUN npm install --silent

