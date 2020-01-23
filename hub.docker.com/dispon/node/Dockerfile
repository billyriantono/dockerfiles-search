FROM debian:buster-slim

RUN apt-get update && apt-get install -y sudo \
    curl \
    gnupg \
    git\
    nano; \
    # Install Node
    curl -sS https://deb.nodesource.com/setup_12.x | sudo -E bash -; \
    apt-get install -y nodejs build-essential; \
    # create initial directory
    mkdir /var/www; \
    mkdir /var/www/html

COPY admin /var/www/html/

WORKDIR /var/www/html/admin

RUN npm install --no-interaction

CMD ["sleep","3600"]
