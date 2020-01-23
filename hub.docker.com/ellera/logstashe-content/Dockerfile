FROM quirky/ruby

# Borrowed from quirky/rails with some minor tweaks.
# MAINTAINER Micah Martin <micahlmartin@gmail.com>

MAINTAINER Eliot Jordan <eliot.jordan@gmail.com>

# Bundler
RUN gem install bundler --version=1.6.2

# Rails
RUN gem install --no-ri --no-rdoc rails --version=4.0.0

# scss-lint
RUN gem install scss-lint

# Nodejs
RUN apt-add-repository ppa:chris-lea/node.js -y && \
    apt-get update -y && \
    apt-get install nodejs -y

# Nodejs tools
RUN npm install -g bower
RUN npm install -g grunt-cli
RUN npm install -g gulp

# PostgreSQL client
RUN apt-get install libpq-dev -y
RUN apt-get install postgresql-client -y

# Mysql client
RUN apt-get install mysql-client libmysqlclient-dev -y

ENTRYPOINT ["/sbin/my_init", "--"]
CMD ["/bin/bash"]