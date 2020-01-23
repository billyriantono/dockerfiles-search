FROM elgalu/selenium:latest

MAINTAINER Andrew Hao <andrew@carbonfive.com>

RUN sudo apt-get update
RUN sudo apt-get -qq update
RUN sudo apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_4.x | sudo bash
RUN sudo apt-get install -y nodejs

CMD ["Image built."]
ENTRYPOINT ["echo"]
