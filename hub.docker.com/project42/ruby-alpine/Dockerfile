FROM project42/base-alpine
MAINTAINER Jordan Clark jordan.clark@esu10.org

RUN apk add --no-cache ca-certificates ruby ruby-io-console && \
echo 'gem: --no-rdoc --no-ri' >/etc/gemrc && \
umask 0022 && \
gem update --system && \
gem install bundler && \
bundle config --global build.nokogiri '--use-system-libraries' && \
bundle config --global disable_shared_gems '1' && \
bundle config --global frozen '1' && \
bundle config --global jobs '8' && \
bundle config --global path 'vendor/bundle' && \
bundle config --global without 'development:test'

ENV COMMAND 'ruby -v'

