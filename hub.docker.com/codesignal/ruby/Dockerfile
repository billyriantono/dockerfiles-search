FROM codesignal/ubuntu-base:v5.0

RUN apt-add-repository ppa:brightbox/ruby-ng \
    && apt-get -qq update \
    && apt-get install --no-install-recommends -y ruby2.5 \
    && apt-get install --no-install-recommends -y ruby`ruby -e 'puts RUBY_VERSION[/\d+\.\d+/]'`-dev libpq-dev \
    && gem install rspec pg mysql2 activemodel activerecord activesupport json faker pry \
    && rm -rf /var/lib/apt/lists/*
