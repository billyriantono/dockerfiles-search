FROM ruby:2.5.0
MAINTAINER rorono <kosuke19952000@gmail.com>

RUN apt-get update -qq \
    && apt-get install -y \
      net-tools \
    && apt-get clean \
    && rm -r /var/lib/apt/lists/*

# init
ENV APP_HOME /app
ENV HOME /root
RUN mkdir $APP_HOME
WORKDIR $APP_HOME

# Install sinatra
RUN gem install sinatra

# Upload source
COPY . $APP_HOME

# Start server
ENV PORT 6000
EXPOSE 6000
CMD ["ruby", "main.rb", "-e", "production"]
