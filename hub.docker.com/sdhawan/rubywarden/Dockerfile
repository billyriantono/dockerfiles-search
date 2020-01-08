FROM ruby:2.2.8

COPY . /srv

WORKDIR /srv

RUN bundle install

RUN mkdir -p /srv/db/production

RUN chmod +x ./entrypoint

ENTRYPOINT [ "./entrypoint" ]

CMD [ "run" ]
