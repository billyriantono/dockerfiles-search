FROM matsudai/ruby:2.5.1

ENV HOME /root

WORKDIR /tmp/bundle
ADD Gemfile ./
ADD Gemfile.lock ./

RUN yum install -y sqlite-devel

RUN source ~/.bash_profile \
    && gem install bundler \
    && bundle

WORKDIR ${HOME}
RUN rm -rf /tmp/bundle
