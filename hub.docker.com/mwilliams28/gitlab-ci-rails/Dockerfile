FROM ruby:2.4.6

RUN apt-get update -qq && apt-get install -y build-essential libxml2-dev libxslt1-dev libqt4-dev xvfb curl software-properties-common
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get update -yq && apt-get install -y nodejs
RUN wget -q -O - https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && echo 'deb https://dl.yarnpkg.com/debian/ stable main' > /etc/apt/sources.list.d/yarn.list
RUN apt-get update -yq && apt-get install -y yarn
RUN yarn install
RUN gem install bundler

CMD ["irb"]