FROM ruby:2.5
ARG WORK_DIR=/rails
ENV work_dir $WORK_DIR
RUN gem install rails
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add 
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update -qq
RUN apt-get install -y sqlite3 libsqlite3-dev nodejs postgresql-client yarn
RUN mkdir -p $work_dir
WORKDIR $work_dir
EXPOSE 3000
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
