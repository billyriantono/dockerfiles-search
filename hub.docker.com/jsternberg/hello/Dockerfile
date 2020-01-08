FROM ubuntu:14.04
MAINTAINER Jonathan A. Sternberg <jonathan.sternberg@knewton.com>
RUN apt-get update && apt-get install -y bundler
RUN useradd -m -d /var/lib/hello hello
ADD . /var/lib/hello
WORKDIR /var/lib/hello
USER hello
RUN bundle install --deployment --without development,test
EXPOSE 5000
ENTRYPOINT ["bundle","exec","ruby","app.rb","-p","5000","-e","production"]
CMD []
