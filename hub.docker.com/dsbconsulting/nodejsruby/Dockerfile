FROM dsbconsulting/nodejs:latest

WORKDIR /

RUN apt-get update && apt-get install -y supervisor g++ git ruby-full rubygems-integration

RUN gem install compass
RUN gem install sass
