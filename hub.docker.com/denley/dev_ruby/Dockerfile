FROM denley/dev_ubuntu
MAINTAINER Denley Hsiao <denley@justtodo.com>

# 安装rvm & ruby
ARG VERSION=2.6.3
RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 7D2BAF1CF37B13E2069D6956105BD0E739499BDB \
  && curl -L https://get.rvm.io | bash -s stable \
  && source  $HOME/.bash_profile \
  && rvm requirements \
  && rvm install ruby-$VERSION \
  && rvm use ruby-$VERSION --default
