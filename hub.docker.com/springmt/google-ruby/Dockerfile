FROM l.gcr.io/google/ruby:latest

RUN cd /rbenv/plugins/ruby-build && \
    git pull && \
    rbenv install -s 2.5.5 && \
    rbenv global 2.5.5 && \
    gem install -q --no-rdoc --no-ri bundler
ENV RBENV_VERSION 2.5.5

CMD [ "irb" ]
