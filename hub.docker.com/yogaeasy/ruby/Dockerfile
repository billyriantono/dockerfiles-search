FROM yogaeasy/ruby:latest

ENV app /vagrant
USER vagrant

COPY Gemfile* /tmp/
WORKDIR /tmp

RUN /bin/bash -c 'source ~/.bashrc \
 && BUNDLE_IGNORE_CONFIG=true \
    bundle config git.allow_insecure true \
 && BUNDLE_IGNORE_CONFIG=true \
 && bundle install --jobs=4'

WORKDIR $app

CMD ["/usr/sbin/sshd", "-D"]
