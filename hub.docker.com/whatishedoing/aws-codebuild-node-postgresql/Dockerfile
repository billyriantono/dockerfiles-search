FROM node:lts

# Update packages, then install base ones.
RUN apt-get update
RUN apt-get install -y apt-transport-https

# Register Yarn repository: https://yarnpkg.com/en/docs/install#debian-stable.
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

# Update again, then install PostgreSQL, Python, Yarn and supporting packages.
RUN apt-get update
RUN apt-get install -y jq locales-all postgresql postgresql-contrib python3-pip yarn

# Install required Node and Python packages.
RUN pip3 install awscli --upgrade
RUN npm install --global npm typescript

# Ensure some base locales are available for database creation.
RUN locale-gen en_GB.UTF-8
RUN locale-gen en_US.UTF-8

# Clean up.
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# This is a build-only image, so no CMD.
