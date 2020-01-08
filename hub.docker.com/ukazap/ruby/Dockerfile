FROM ukazap/ruby:prod-bionic-2.6.3

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
    apt update && apt install -y build-essential zlib1g-dev nodejs && \
    apt clean && apt autoclean && \
    npm install -g yarn