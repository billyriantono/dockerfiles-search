FROM ruby:2.5

RUN mkdir /users_ms
WORKDIR /users_ms

ADD Gemfile /users_ms/Gemfile
ADD Gemfile.lock /users_ms/Gemfile.lock

RUN bundle install
ADD . /users_ms
RUN apt update 
RUN apt install mysql-client -y
EXPOSE 3009
RUN chmod +x entrypoint.sh
CMD "./entrypoint.sh"
#CMD "sleep 10 && rails db:create && rails db:migrate && rails s -p 3009 -b '0.0.0.0'"