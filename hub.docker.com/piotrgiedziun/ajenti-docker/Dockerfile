FROM ubuntu:latest

RUN apt-get update && apt-get install -y curl

RUN curl https://raw.githubusercontent.com/ajenti/ajenti/master/scripts/install.sh | bash -s -

EXPOSE 8000 21