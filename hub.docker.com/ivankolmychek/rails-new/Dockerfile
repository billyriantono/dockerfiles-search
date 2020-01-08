FROM ruby:2.3

RUN useradd -m -u 1000 user

RUN gem install rails -v '~> 5.0' --no-rdoc --no-ri

USER user

CMD /bin/bash
