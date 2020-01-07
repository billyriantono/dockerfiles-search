FROM zyps/base-build:latest

# Add package repositories for NodeJS and Yarn
RUN add-apt-repository "deb https://dl.yarnpkg.com/debian/ stable main" \
  && curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
  && apt-get update \
  && curl -sL https://deb.nodesource.com/setup_12.x | bash - \
# Install
  && apt-get install -y nodejs yarn \
# Clean
  && rm -rf /var/lib/apt/lists/*
