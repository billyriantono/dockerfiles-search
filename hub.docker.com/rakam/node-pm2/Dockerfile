FROM ubuntu:14.04

RUN apt-get -qq update
RUN apt-get install -qq -y curl

# Install NodeJS 4
RUN curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
RUN apt-get install -y nodejs

# Install pm2
RUN npm install -g pm2@1.0.0

VOLUME ["/app"]
ADD launch /launch
RUN chmod 755 /launch

EXPOSE 80
EXPOSE 443
EXPOSE 5858
EXPOSE 8080