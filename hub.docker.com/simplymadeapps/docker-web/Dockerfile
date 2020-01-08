FROM heroku/heroku:18

# install apt based dependencies required to run Rails as
# well as RubyGems. As the Ruby image itself is based on a
# Debian image, we use apt-get to install those.
RUN export DEBIAN_FRONTEND=noninteractive && apt-get update && apt-get install -qq --yes build-essential nodejs libpq-dev git tzdata libxml2-dev libxslt-dev libssl-dev openjdk-8-jdk ssh net-tools

# install Ruby and RubyGems
RUN wget http://ftp.ruby-lang.org/pub/ruby/2.6/ruby-2.6.5.tar.gz && \
tar -xzvf ruby-2.6.5.tar.gz && \
cd ruby-2.6.5/ && \
./configure && \
make -j4 && \
make install && \
ruby -v

# install bundler
RUN gem install bundler -v '=2.0.2'

# install Node
RUN wget https://nodejs.org/dist/v10.16.3/node-v10.16.3.tar.gz && \
tar -xzvf node-v10.16.3.tar.gz && \
rm node-v10.16.3.tar.gz && \
cd node-v10.16.3 && \
./configure && \
make -j4 && \
make install && \
cd .. && \
rm -r node-v10.16.3

# install Yarn via yvm
ARG yarnversion=1.17.3
RUN curl -fsSL https://raw.githubusercontent.com/tophat/yvm/master/scripts/install.sh | bash
RUN ~/.yvm/yvm.sh install $yarnversion
ENV PATH="/root/.yvm/versions/v${yarnversion}/bin:${PATH}"

# install Heroku
RUN wget https://cli-assets.heroku.com/heroku-linux-x64.tar.gz
RUN mkdir -p /usr/local/lib /usr/local/bin
RUN tar -xvzf heroku-linux-x64.tar.gz -C /usr/local/lib
RUN ln -s /usr/local/lib/heroku/bin/heroku /usr/local/bin/heroku

# install Postgres clients
RUN apt-get update && apt-get -y install postgresql-client

RUN curl --silent --show-error --location --fail --retry 3 --output /tmp/google-chrome-stable_current_amd64.deb https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
  && (dpkg -i /tmp/google-chrome-stable_current_amd64.deb || apt-get update && apt-get -fy install)  \
  && rm -rf /tmp/google-chrome-stable_current_amd64.deb \
  && sed -i 's|HERE/chrome"|HERE/chrome" --disable-setuid-sandbox --no-sandbox|g' \
     "/opt/google/chrome/google-chrome"

RUN apt-get update && apt-get -y install libgconf-2-4 \
  && curl --silent --show-error --location --fail --retry 3 --output /tmp/chromedriver_linux64.zip "https://chromedriver.storage.googleapis.com/76.0.3809.68/chromedriver_linux64.zip" \
  && cd /tmp \
  && unzip chromedriver_linux64.zip \
  && rm -rf chromedriver_linux64.zip \
  && mv chromedriver /usr/local/bin/chromedriver \
  && chmod +x /usr/local/bin/chromedriver

# Busting up the apt cache and removing the contents of
# /var/lib/apt/lists helps us keep the image size down.
RUN rm -rf /var/lib/apt/lists/*

# Configure the main working directory. This is the base
# directory used in any further RUN, COPY, and ENTRYPOINT
# commands.
WORKDIR /opt/webapp
