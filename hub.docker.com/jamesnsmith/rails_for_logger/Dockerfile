FROM ruby:2.3

WORKDIR /app
COPY . /app

RUN apt-get update -qq && apt-get install -y nodejs mysql-client
RUN gem install rails -v 5.2.3
RUN gem install bundler -v 2.0.1
RUN bundle update
RUN bundle install

RUN bundler -v
RUN rails -v

# Add a script to be executed every time the container starts.
#RUN chmod +x /usr/bin/entrypoint.sh
#ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000 3306

RUN git clone https://github.com/jamesnsmith/loggerv2.git
WORKDIR /app/loggerv2
RUN bundle install

# Start the main process.
CMD ["rails", "server", "-b", "0.0.0.0"]

#####################################
#FROM ruby:2.3
#RUN apt-get update -qq && apt-get install -y nodejs mysql-client
#RUN mkdir /myapp
#WORKDIR /myapp
#COPY Gemfile /myapp/Gemfile
#COPY Gemfile.lock /myapp/Gemfile.lock
#RUN bundle install
#COPY . /myapp

# Add a script to be executed every time the container starts.
#COPY entrypoint.sh /usr/bin/
#RUN chmod +x /usr/bin/entrypoint.sh
#ENTRYPOINT ["entrypoint.sh"]
#EXPOSE 3000 3306

# Start the main process.
#RUN rails -v
#CMD ["rails", "server", "-b", "0.0.0.0"]

#FROM ruby:2.3#
#FROM buildpack-deps:stretch
#Ruby
#RUN curl -sL https://deb.nodesource.com/setup_8.x \
#    && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
#    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list 

#RUN apt-get update \
    #&& apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common libffi-dev nodejs yarn

#Rbenv
#RUN git clone https://github.com/rbenv/rbenv.git ~/.rbenv \
#    && echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc \
#    && echo 'eval "$(rbenv init -)"' >> ~/.bashrc \
#    && exec $SHELL

#RUN git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build \
#    && echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc \
#    && exec $SHELL 

#RUN rbenv install 2.6.1 #2.3.3
#RUN rbenv global 2.6.1
#RUN ruby -v

#RUN gem install bundler

#Rails
#RUN curl -sL https://deb.nodesource.com/setup_8.x | -E bash - 
#RUN apt-get install -y nodejs

#RUN gem install rails -v 5.2.2 #5.1.7

#RUN rbenv rehash

#RUN rails -v

#mysql
#RUN apt-get install mysql-server mysql-client libmysqlclient-dev

#EXPOSE 3000
#CMD ["rails", "server", "-b", "0.0.0.0"]

#FROM ruby:2.3

#WORKDIR /usr/src/app
#COPY Gemfile* ./
#RUN bundle install
#COPY . .

