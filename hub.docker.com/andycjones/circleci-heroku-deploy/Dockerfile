FROM openjdk

RUN wget -qO- https://cli-assets.heroku.com/install-ubuntu.sh | sh
RUN heroku plugins:install heroku-cli-deploy
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs
