FROM buildkite/puppeteer:v1.11.0

# https://superuser.com/a/1423685/217405
RUN printf "deb http://archive.debian.org/debian/ jessie main\ndeb-src http://archive.debian.org/debian/ jessie main\ndeb http://security.debian.org jessie/updates main\ndeb-src http://security.debian.org jessie/updates main" > /etc/apt/sources.list

RUN apt-get update
RUN apt-get -y install procps
RUN apt-get -y install curl
RUN apt-get -y install git
