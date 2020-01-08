FROM ruby:2.4.3-stretch
RUN apt-get update -qq && apt-get install -y build-essential curl redis-server
RUN curl https://getcaddy.com | bash -s personal
RUN chown root:root /usr/local/bin/caddy && chmod 755 /usr/local/bin/caddy
RUN mkdir /home/hyperforms-api
WORKDIR /home/hyperforms-api
COPY . ./
RUN bundle install
RUN redis-server &
#RUN EDITOR=nano rails credentials:edit

#ENV RAILS_ENV=production
#ENV RAKE_ENV=production

EXPOSE 3000
#CMD ["caddy"]
CMD ["bundle", "exec", "rails", "s"]