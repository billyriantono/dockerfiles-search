FROM ruby:2

RUN gem install redis-browser

RUN apt-get update -yq && apt-get upgrade -yq && apt-get install nodejs -yq

EXPOSE 80

CMD ["redis-browser", "--port", "80"]