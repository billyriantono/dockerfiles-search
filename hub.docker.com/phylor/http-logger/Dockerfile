FROM ruby

RUN gem install thin
COPY config.ru /srv/config.ru
WORKDIR /srv

CMD ["thin", "start", "-p", "80", "-D", "-V"]
