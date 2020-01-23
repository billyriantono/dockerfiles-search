FROM ruby:2.2.7-alpine

RUN apk --update add build-base postgresql-dev
RUN gem install gitrob

RUN touch /usr/local/bundle/gems/gitrob-1.1.2/agreement.txt

COPY .gitrobrc /root/.gitrobrc

CMD gitrob server --bind-address=0.0.0.0 --port=9393