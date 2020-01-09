FROM michilu/fedora-ruby

COPY Gemfile Gemfile
RUN \
  bundle install --jobs `grep processor /proc/cpuinfo|wc -l` &&\
  rm Gemfile
