FROM ruby:2.2.3
MAINTAINER Oleg Kulyk

ENV HOME="/root" \
    SERVICE_NAME="Heroku Toolbelt" \
    CONTAINER_PS1="[ $(get_container_ip) | \[\e[0;36m\]$(get_container_service)\[\e[m\] | \[\e[0;35m\]\w\[\e[m\] ]\n\[\e[1;31m\]>\[\e[m\] "

COPY .container_home/ $HOME/

# Install Heroku CLI client
RUN mkdir -p /usr/src/app \
  && mkdir -p /usr/local/heroku \
  && cd /usr/local/heroku \
  && wget -qO- "https://s3.amazonaws.com/assets.heroku.com/heroku-client/heroku-client.tgz" | tar xz \
  && mv heroku-client/* . \
  && rmdir heroku-client

WORKDIR /usr/src/app

CMD ["/bin/bash"]
