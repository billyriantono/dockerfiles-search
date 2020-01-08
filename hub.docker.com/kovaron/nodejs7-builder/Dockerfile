FROM ubuntu

RUN apt-get update -qq && \
	apt-get install -qq -y curl

ENV LANG C.UTF-8

RUN curl -sL https://deb.nodesource.com/setup_7.x | bash -
RUN apt-get update -qq && apt-get install -qq -y nodejs