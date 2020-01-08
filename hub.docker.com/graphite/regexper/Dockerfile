FROM node

RUN apt-get update && apt-get install -y \
  bundler

RUN git clone https://github.com/javallone/regexper-static
RUN cd /regexper-static && bundle install && npm install
RUN cd /regexper-static && npm install -g gulp && gulp build

CMD cd /regexper-static && gulp server

EXPOSE 8080
