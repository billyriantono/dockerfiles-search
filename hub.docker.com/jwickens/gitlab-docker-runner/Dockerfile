FROM gitlab/gitlab-runner:ubuntu-v9.3.0

# Install Cloud foundry
RUN wget -q -O - https://packages.cloudfoundry.org/debian/cli.cloudfoundry.org.key | sudo apt-key add - \
    && echo "deb http://packages.cloudfoundry.org/debian stable main" | sudo tee /etc/apt/sources.list.d/cloudfoundry-cli.list \
    && apt-get update \
    && sudo apt-get install cf-cli

# Install docker
RUN sudo curl -sSL https://get.docker.com/ | sh \
    && sudo usermod -aG docker gitlab-runner

COPY docker-entrypoint /

# Install nodejs, npm 
RUN wget -q -O - https://deb.nodesource.com/setup_8.x | sudo -E bash - \
    && sudo apt-get install nodejs -y \
    && node --version

# Install yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list \
    && sudo apt-get update && sudo apt-get install -y yarn \
    && yarn --version

ENTRYPOINT ["/usr/bin/dumb-init","/docker-entrypoint"]
CMD ["run", "--user=gitlab-runner", "--working-directory=/home/gitlab-runner"]