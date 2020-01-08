FROM ruby:2.4.2

RUN apt-get update && apt-get -y --no-install-recommends install postgresql-client
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash
RUN apt-get install -y nodejs
RUN apt-get update && apt-get install -y curl apt-transport-https wget && \
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
apt-get update && apt-get install -y yarn

ENV APP_USER rails
ENV APP_HOME /app

RUN useradd  --create-home --shell /bin/bash $APP_USER

RUN mkdir -p $APP_HOME

RUN chown -R $APP_USER $APP_HOME
RUN chown -R $APP_USER /usr/local/bundle

WORKDIR $APP_HOME

USER $APP_USER

CMD ["bundle", "exec", "rails", "server", "-b", "0.0.0.0"]
