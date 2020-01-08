FROM tcnksm/centos-ruby:2.1

# throw errors if Gemfile has been modified since Gemfile.lock
RUN bundle config --global frozen 1

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

ONBUILD COPY Gemfile /usr/src/app/
ONBUILD COPY Gemfile.lock /usr/src/app/
ONBUILD RUN bundle install

ONBUILD COPY . /usr/src/app

RUN yum update && yum install -y nodejs && yum clean all

# see http://guides.rubyonrails.org/command_line.html#rails-dbconsole
RUN yum update && yum install -y mysql postgresql sqlite && yum clean all

EXPOSE 3000
CMD ["rails", "server"]
