FROM ruby:2.3.1
WORKDIR /git-build
RUN apt-get update \
  && apt-get install -y libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev \
  && wget https://github.com/git/git/archive/v2.17.1.tar.gz \
  && tar -zxf v2.17.1.tar.gz
WORKDIR /git-build/git-2.17.1
RUN make prefix=/usr all \
    && make prefix=/usr install \
    && rm -rf /git-build \
    && apt-get remove -y libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev
CMD git --version
