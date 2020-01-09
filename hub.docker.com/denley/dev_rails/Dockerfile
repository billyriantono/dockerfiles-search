FROM denley/dev_ruby
MAINTAINER Denley Hsiao <denley@justtodo.com>

# 安装rails
ARG VERSION=5.2.3
RUN source  $HOME/.bash_profile \
  && gem install rails -v $VERSION

ENV HOME=/home/denley
ENV CURR_DIR=$HOME/app
RUN mkdir -p $CURR_DIR
WORKDIR $CURR_DIR

ONBUILD COPY Gemfile $CURR_DIR
ONBUILD COPY Gemfile.lock $CURR_DIR
ONBUILD RUN source $HOME/.bash_profile \
  && sudo chmod a+w $CURR_DIR/Gemfile.lock \
  && bundle install

EXPOSE 3000
CMD ["bash", "-c", "source $HOME/.bash_profile; rails s -e production -b 0.0.0.0"]
