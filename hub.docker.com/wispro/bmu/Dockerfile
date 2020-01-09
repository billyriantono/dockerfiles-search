FROM ruby:2.6-alpine3.10
# alpine3.9 tiene un iproute2 que no funciona desde docker

# Patch to get global bins
ENV BUNDLE_BIN="$GEM_HOME/bin"
ENV PATH $BUNDLE_BIN:$PATH
RUN mkdir -p "$BUNDLE_BIN"
RUN chmod 777 "$BUNDLE_BIN"

RUN echo "gem: --no-rdoc --no-ri" >> ~/.gemrc && \
    apk --update add --virtual build-dependencies build-base python bison flex && \
    apk --update add bash tzdata git openssh postgresql-dev sqlite-dev rsync \
                     curl ethtool fping conntrack-tools mii-tool iptables ipset \
                     nodejs npm coreutils iperf3 && \
    gem install bundler && \
    mkdir -m 700 -p /root/.ssh && \
    ssh-keyscan github.com >> ~/.ssh/known_hosts

WORKDIR /usr/src/app

COPY .irbrc /root/.irbrc

COPY Gemfile Gemfile.lock .keys/docker-rsa-utils .keys/docker-rsa-frontend .keys/custom-git-ssh ./

RUN chmod 600 docker-rsa-frontend docker-rsa-utils

RUN GIT_SSH=/usr/src/app/custom-git-ssh NO_SSL=true bundle install --without development test --deployment --jobs 8

RUN cd /tmp && \
    wget https://sourceforge.net/projects/iperf2/files/iperf-2.0.13.tar.gz/download -c -O iperf-2.tar.gz && \
    tar xzf iperf-2.tar.gz && \
    cd /tmp/iperf-2.0.13 && ./configure && make && make install &&\
    cd /tmp && \
    git clone git://git.kernel.org/pub/scm/network/iproute2/iproute2.git && \
    cd iproute2 && \
    ./configure && make && make install && \
    cd / && rm -Rf /tmp/ip* && \
    apk del build-dependencies

ADD . ./

ENV RAILS_ENV=production
ENV SECRET_KEY_BASE=123

RUN npm config set unsafe-perm true && npm install yarn -g && yarn install && bundle exec rails assets:precompile
RUN mkdir -p tmp/sockets
CMD ["/usr/src/app/bin/docker-cmd-server.sh"]
