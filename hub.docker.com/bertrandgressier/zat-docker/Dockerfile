FROM ruby:latest

ENV LC_CTYPE=C.UTF-8
ENV LANGUAGE C.UTF-8
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

RUN gem install rake

RUN gem install zendesk_apps_tools

# Install Node.js
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash
RUN apt-get install --yes nodejs
RUN node -v
RUN npm -v

WORKDIR /data

EXPOSE 4567

ENTRYPOINT ["zat"]
