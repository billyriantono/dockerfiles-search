FROM sot528/vyper:v0.1.0-beta.6

RUN apt-get update
RUN apt-get install -y vim git curl gnupg gnupg1 gnupg2

ENTRYPOINT /bin/bash

# Node.js + npm
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -y nodejs
RUN npm install npm@latest -g

# Truffle
RUN npm install truffle -g
RUN truffle unbox vyper-example
RUN truffle compile