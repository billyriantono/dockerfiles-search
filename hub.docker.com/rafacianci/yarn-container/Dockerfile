FROM debian:sid
RUN apt-get update --fix-missing \
    && apt-get install -y curl \
    && apt-get install -y gnupg \
    && curl -sL https://deb.nodesource.com/setup_4.x | bash - \
    && apt-get install -y nodejs \
    && curl -o- -L https://yarnpkg.com/install.sh | bash
