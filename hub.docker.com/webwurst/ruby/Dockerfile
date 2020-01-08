from webwurst/ubuntu
run apt-get update

# some ruby dependencies
run apt-get -y install build-essential zlib1g-dev libssl-dev libreadline-dev libdevil-dev libsqlite3-dev libmysqlclient-dev freetds-dev libxslt1-dev libxml2-dev libffi-dev nodejs

# ruby
run cd /tmp && git clone https://github.com/sstephenson/ruby-build.git
run /tmp/ruby-build/install.sh
# ruby-build --definitions
run ruby-build 2.1.2 /usr/local

# bundler
run gem install bundler
