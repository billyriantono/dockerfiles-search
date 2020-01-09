FROM ruby:latest

# install deps (notable sinatra)
COPY src/Gemfile /src/Gemfile
RUN cd /src ; bundle install

COPY ./src /src/

EXPOSE 4567 
CMD ["ruby", "/src/hello.rb"]
