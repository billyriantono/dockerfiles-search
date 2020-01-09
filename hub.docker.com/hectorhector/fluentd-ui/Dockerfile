FROM ruby:2.6.2

EXPOSE 24224

EXPOSE 9292

VOLUME ["/root"]

RUN gem install --no-document fluentd-ui
RUN fluentd-ui setup

CMD ["fluentd-ui", "start"]
