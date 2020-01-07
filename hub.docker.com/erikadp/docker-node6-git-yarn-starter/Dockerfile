FROM node:6

# Can't install yarn without this
RUN apt-get update && apt-get install apt-transport-https

# Install yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
&& echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
&& apt-get update \
&& apt-get install yarn \
&& apt-get -y install git-all \
&& yarn global add grunt-cli \
&& yarn global add gulp
