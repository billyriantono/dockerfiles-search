FROM ruby

RUN apt-get -y update
RUN apt-get -y install build-essential python python-docutils libicu-dev libreadline-dev libssl-dev zlib1g-dev git-core
RUN apt-get clean && \
    rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

WORKDIR /wiki

RUN gem install redcarpet github-markdown

COPY Gemfile /wiki/

RUN bundle install

RUN git config --global user.name  "root@dev.netartz.com" &&\
    git config --global user.email "root"
RUN git init
RUN git config core.quotepath false
RUN git add Gemfile*
RUN git commit -m 'Add Gemfile'

EXPOSE 4567

CMD ["gollum", "--port", "4567"]
