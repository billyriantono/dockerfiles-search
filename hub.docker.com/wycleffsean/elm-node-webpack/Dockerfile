FROM codesimple/elm:0.18

# Apt https method
RUN \
  apt-get update && apt-get install -y apt-transport-https

# Install Yarn
RUN \
  curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
  && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
  && apt-get update && apt-get install yarn

WORKDIR /usr/app

RUN mkdir -p /usr/app/src /usr/app/build

COPY ./package.json package.json
COPY ./yarn.lock yarn.lock

# Install Dependencies
RUN yarn install && yarn global add webpack@3.1.0

ENTRYPOINT []
CMD ['webpack', 'run'] 
