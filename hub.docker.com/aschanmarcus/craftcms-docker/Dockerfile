FROM wyveo/craftcms-docker:3.3.15

ENV APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=DontWarn

# Add Ansible repository
RUN echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" | tee /etc/apt/sources.list.d/ansible.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367

# Add Yarn repository
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

# Add NodeJS repository
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -

# Install packages
RUN apt-get update && apt-get install -y \
        unzip \
        yarn \
        nodejs \
        openssh-client \
        rsync \
        ansible

# Install NVM
RUN curl -sL https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash -

# Install Ansistrano
RUN ansible-galaxy install ansistrano.deploy ansistrano.rollback
