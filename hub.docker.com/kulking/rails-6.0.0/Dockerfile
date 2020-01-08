FROM kulking/ruby-2.6.4
RUN gem install rails -v 6.0.0; \
echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections; \
apt-get install -y libmysqlclient-dev curl; \
curl -sL https://deb.nodesource.com/setup_12.x | bash -; \
apt-get install -y nodejs; \
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -; \
echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list; \
apt-get -y update; \
apt-get install -y yarn; \
apt-get install -y tzdata