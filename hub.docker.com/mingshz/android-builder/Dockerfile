FROM musichin/build-environment-android

RUN apt-get update
RUN apt-get install -y ssh rsync
RUN apt-get install gnupg2 -y
RUN gpg --keyserver hkp://pool.sks-keyservers.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
RUN curl -sSL https://get.rvm.io | bash -s stable
RUN /usr/local/rvm/bin/rvm install 2.6.3
RUN /usr/local/rvm/bin/rvm use 2.6.3
ENV PATH="/usr/local/rvm/gems/ruby-2.6.3/bin:/usr/local/rvm/gems/ruby-2.6.3@global/bin:/usr/local/rvm/rubies/ruby-2.6.3/bin:${PATH}"
RUN ruby -v
# RUN gem install bundler
RUN bundle -v

# Clean up apt-get
RUN rm -rf /var/lib/apt/lists/*
RUN apt-get clean
