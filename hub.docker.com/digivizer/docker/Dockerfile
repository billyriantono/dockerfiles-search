FROM ruby:2.1

RUN curl -sL https://deb.nodesource.com/setup_6.x -o nodesource_setup.sh
RUN bash nodesource_setup.sh

RUN wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list

RUN DEBIAN_FRONTEND=noninteractive apt-get -y -q update && apt-get -y -q install libxapian-dev nodejs protobuf-compiler=2.6.1-1 apt-utils build-essential libpq-dev postgresql-client libpython-dev python-pip groff-base jq google-chrome-stable xvfb
RUN /usr/sbin/update-alternatives --quiet --install /usr/bin/node node /usr/bin/nodejs 10

# Disable Chrome Sandbox due to kernel issues
RUN sed -i 's|HERE/chrome"|HERE/chrome" --disable-setuid-sandbox --no-sandbox|g' "/opt/google/chrome/google-chrome"

# Install AWS CLI tools
RUN pip install awscli

# set up app environment
ENV APP_HOME /usr/share/dgvz
ENV DISPLAY :99
ENV NODE_PATH /usr/lib/node_modules

# set up our app
RUN mkdir -p $APP_HOME
WORKDIR $APP_HOME
