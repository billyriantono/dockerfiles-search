FROM intxlog/ubuntu1804

RUN echo "deb https://deb.nodesource.com/node_8.x bionic main" >> /etc/apt/sources.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 68576280

RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" >> /etc/apt/sources.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 46C2130DFD2497F5

RUN apt-get update

RUN apt-get install --assume-yes --no-install-recommends --no-install-suggests \
    build-essential \
    nodejs \
    yarn

RUN apt-get purge --assume-yes --auto-remove \
    --option APT::AutoRemove::RecommendsImportant=false \
    --option APT::AutoRemove::SuggestsImportant=false
RUN rm -rf /var/lib/apt/lists/*

ENV NODE_PATH /usr/lib/node_modules
