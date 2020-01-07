FROM ruby:2.2.0

RUN  apt-get update
RUN  apt-get install -y nodejs

# RUN  git clone https://github.com/rustyio/super-imap.git /superimap
COPY super-imap /superimap
WORKDIR /superimap

RUN  pwd
RUN  ls -l
COPY database.yml /superimap/config/

RUN  bundle

ENV  SECRET_KEY_BASE r87wNeUas9SDhHsQ
ENV  ENCRYPTION_KEY  KgZUTudqtVu4VN6w
ENV  RAILS_ENV       default

CMD  [ "sh","-c", "rake db:setup db:seed && RAILS_ENV=production bundle exec rails c" ]
#CMD  [ "sh","-c", "rake db:setup db:seed && foreman start -c 'web=1, worker=1, imap_client_1x=1'" ]