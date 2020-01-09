FROM ruby

RUN gem install s3_website

RUN apt-get update
RUN apt remove cmdtest
RUN apt-get install -y openjdk-8-jre-headless nodejs

RUN ln -s /usr/bin/nodejs /usr/bin/node

# Install yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN DEBIAN_FRONTEND=noninteractive apt-get install -qy apt-transport-https
RUN apt-get update && apt-get install yarn

VOLUME ["/website", "/config"]

WORKDIR /website

ENTRYPOINT ["s3_website"]

CMD ["--help"]