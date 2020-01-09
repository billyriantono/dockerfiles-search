FROM starefossen/ruby-node:2-10

# install compass
RUN gem install compass
RUN gem install bundler

# grunt and bower
RUN npm install -g grunt-cli bower
RUN npm install -g cf-cli
RUN wget -O /tmp/cf-cli.tgz "https://cli.run.pivotal.io/stable?release=linux64-binary&version=6.34.1" #current version of cli is 6.31.0
RUN mkdir -p /usr/local/bin
RUN tar -xzf /tmp/cf-cli.tgz -C /usr/local/bin
RUN cf add-plugin-repo CF-Community https://plugins.cloudfoundry.org
RUN cf install-plugin blue-green-deploy -r CF-Community -f