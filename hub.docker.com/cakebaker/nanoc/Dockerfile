FROM ruby:2.2.2
MAINTAINER Daniel Hofstetter (daniel.hofstetter@42dh.com)

RUN apt-get update \
        && apt-get install -y --no-install-recommends \
               rsync

RUN gem install nanoc \
                kramdown \
                nokogiri \
                sass \
                w3c_validators

RUN useradd nanoc
RUN mkdir /data
RUN chown nanoc /data
USER nanoc
WORKDIR /data
ENTRYPOINT ["nanoc"]
