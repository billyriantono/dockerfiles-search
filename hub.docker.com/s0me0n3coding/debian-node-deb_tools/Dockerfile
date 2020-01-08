FROM debian:latest

RUN rm -f /etc/apt/apt.conf.d/docker-clean

RUN apt-get update && apt-get -y --no-upgrade --no-remove --no-install-recommends install curl gnupg ca-certificates

RUN curl -skS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -

RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

RUN apt-get update && apt-get -y --no-install-recommends --no-upgrade --no-remove install debhelper yarn net-tools git g++ build-essential devscripts fakeroot

RUN curl -sL https://deb.nodesource.com/setup_11.x  | bash -

RUN apt-get -y install nodejs

RUN rm -rf /var/lib/apt/lists/*

RUN apt-get clean
