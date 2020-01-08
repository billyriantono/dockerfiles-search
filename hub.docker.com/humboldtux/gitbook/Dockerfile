FROM node
MAINTAINER Benoît Benedetti <benoit.benedetti@gmail.com>

ENV REFRESHED_AT 2015-01-01

RUN apt-get -y update

RUN npm install gitbook -g

# Support gitbook pdf
RUN apt-get install -y calibre

VOLUME /repository
WORKDIR /repository

EXPOSE 4000 35729

ENTRYPOINT ["gitbook"]
CMD ["--version"]
