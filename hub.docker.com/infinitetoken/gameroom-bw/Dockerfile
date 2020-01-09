FROM athurg/alpine-ruby-1.9.3

ENV APP_HOME /gameroom-bw

RUN apk add --no-cache --update build-base \
                                sqlite \
                                sqlite-dev \
                                sqlite-libs \
                                libffi-dev

RUN mkdir $APP_HOME
WORKDIR $APP_HOME

ADD Gemfile* $APP_HOME/
RUN bundle install

ADD . $APP_HOME

COPY docker-entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/docker-entrypoint.sh
ENTRYPOINT ["docker-entrypoint.sh"]
EXPOSE 3000

CMD ["bundle", "exec", "rails", "s", "-b", "0.0.0.0"]
