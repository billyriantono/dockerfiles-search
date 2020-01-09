FROM ruby:2.3

RUN apt-get update -y && \
    apt-get install -y nodejs vim zip && \
	wget https://github.com/innoq/iqvoc/archive/v4.8.2.zip && \
    unzip v4.8.2.zip && \
	cd /iqvoc-4.8.2 && \ 
    bundle install && \
	cp config/database.yml.sqlite config/database.yml && \
	bundle exec rake db:create && \
	rake db:migrate && \
	rake db:seed 

EXPOSE 3000
WORKDIR /iqvoc-4.8.2
CMD ["bundle", "exec", "rails", "server", "-b", "0.0.0.0"] 
