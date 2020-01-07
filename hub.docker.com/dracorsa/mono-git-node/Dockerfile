FROM dracorsa/mono-git:latest
USER root
ENV CI true
ENV NPM_VERSION latest
RUN apt-get -q update && \
    apt-get install -y apt-transport-https

RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -

RUN apt-get -q update && \
    apt-get install -y --force-yes \
    build-essential \
    libsecret-1-dev \
    nodejs \
    yarn \
    && rm -rf /var/lib/apt/lists/* /tmp/*

RUN npm install -g gulp-cli
RUN npm install npm@$NPM_VERSION -g

USER gitlabci
