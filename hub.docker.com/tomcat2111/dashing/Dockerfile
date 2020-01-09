FROM ruby:2.3
  
MAINTAINER Thomas Stägemann <staegi@github.com>

RUN apt-get update && apt-get install nodejs -y
RUN gem install dashing bundler
RUN dashing new dashboard

VOLUME /dashboard
WORKDIR /dashboard

RUN bundle

EXPOSE 3030

CMD ["dashing", "start"]
