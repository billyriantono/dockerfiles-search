from ubuntu

run apt-get update && apt-get install -y \
	ruby ruby-dev zlib1g-dev \
	libz-dev build-essential dh-autoreconf
run gem install bundler
copy . /osquery
run cd /osquery/docs && bundle install
workdir /osquery/docs
cmd bundle exec jekyll serve

