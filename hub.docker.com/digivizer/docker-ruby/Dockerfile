FROM ruby:2.4-stretch as protoc

# build protoc 2.6.1
WORKDIR /tmp
RUN DEBIAN_FRONTEND=noninteractive apt-get -y -q update && apt-get -y -q install build-essential
RUN wget https://github.com/google/protobuf/releases/download/v2.6.1/protobuf-2.6.1.tar.gz
RUN tar xzf protobuf-2.6.1.tar.gz

WORKDIR /tmp/protobuf-2.6.1
RUN ./configure
RUN make
# RUN make check
RUN make install
RUN which protoc

FROM ruby:2.4-stretch

RUN DEBIAN_FRONTEND=noninteractive apt-get -y -q update && apt-get -y -q install awscli debian-archive-keyring apt-transport-https unzip htop vim postgresql-client

# add and cache the gems
RUN gem install bundler
COPY Gemfile $APP_HOME/
COPY Gemfile.lock $APP_HOME/
RUN bundle install

COPY --from=protoc /usr/local/bin/protoc /usr/local/bin/protoc
COPY --from=protoc /usr/local/lib/libprotobuf.so.9 /usr/local/lib/libprotobuf.so.9
COPY --from=protoc /usr/local/lib/libprotoc.so.9 /usr/local/lib/libprotoc.so.9
RUN ldconfig

ENV APP_HOME /usr/share/dgvz
WORKDIR $APP_HOME

# Load App
COPY . $APP_HOME
